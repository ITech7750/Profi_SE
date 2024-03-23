## <p class="center" id="title1" > **Информационная система
для автоматизации их работы специалистов по подбору персонала**</p>
```mysql
create database profi_db;
use profi_db;

CREATE TABLE Company (
                         company_id INT PRIMARY KEY AUTO_INCREMENT,
                         company_name VARCHAR(100) NOT NULL,
                         legal_entity_name VARCHAR(100) NOT NULL,
                         legal_entity_address VARCHAR(100) NOT NULL,
                         contact_phone VARCHAR(20),
                         contact_email VARCHAR(50)
);

CREATE TABLE Vacancy (
                         vacancy_id INT PRIMARY KEY AUTO_INCREMENT,
                         company_id INT,
                         vacancy_title VARCHAR(100) NOT NULL,
                         description TEXT,
                         required_education_level VARCHAR(50),
                         posting_date DATE,
                         application_deadline DATE,
                         salary_range VARCHAR(50),
                         FOREIGN KEY (company_id) REFERENCES Company(company_id)
);

CREATE TABLE Skill (
                       skill_id INT PRIMARY KEY AUTO_INCREMENT,
                       skill_name VARCHAR(50)
);

CREATE TABLE Vacancy_Skill (
                               vacancy_id INT,
                               skill_id INT,
                               PRIMARY KEY (vacancy_id, skill_id),
                               FOREIGN KEY (vacancy_id) REFERENCES Vacancy(vacancy_id),
                               FOREIGN KEY (skill_id) REFERENCES Skill(skill_id)
);

CREATE TABLE Applicant (
                           applicant_id INT PRIMARY KEY AUTO_INCREMENT,
                           full_name VARCHAR(100) NOT NULL,
                           phone_number VARCHAR(20),
                           education_level VARCHAR(50),
                           desired_salary DECIMAL(10, 2),
                           current_vacancy INT,
                           current_employer VARCHAR(100),
                           UNIQUE (full_name)
);

CREATE TABLE Applicant_Skill (
                                 applicant_id INT,
                                 skill_id INT,
                                 PRIMARY KEY (applicant_id, skill_id),
                                 FOREIGN KEY (applicant_id) REFERENCES Applicant(applicant_id),
                                 FOREIGN KEY (skill_id) REFERENCES Skill(skill_id)
);

CREATE TABLE HiringProcess (
                               process_id INT PRIMARY KEY AUTO_INCREMENT,
                               applicant_id INT,
                               interview_dates VARCHAR(100),
                               start_date DATE,
                               current_status VARCHAR(50),
                               FOREIGN KEY (applicant_id) REFERENCES Applicant(applicant_id)
);

CREATE TABLE EmploymentHistory (
                                   history_id INT PRIMARY KEY AUTO_INCREMENT,
                                   applicant_id INT,
                                   start_date DATE,
                                   end_date DATE,
                                   employer_name VARCHAR(100),
                                   FOREIGN KEY (applicant_id) REFERENCES Applicant(applicant_id)
);
```
