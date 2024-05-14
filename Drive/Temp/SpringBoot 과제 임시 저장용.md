# 문제 1.manager 테이블 생성  
CREATE TABLE MANAGER  
(  
    id BIGINT PRIMARY KEY,  
    name VARCHAR(100) NOT NULL,  
    CONSTRAINT manager_ck_name CHECK (length(name) >= 2),  
    student_code VARCHAR(100) NOT NULL,  
    CONSTRAINT manager_fk_student_code FOREIGN KEY (student_code) REFERENCES student(student_code)  
  
);  
  
# 문제 2.ALTER와 MODIFY를 사용하여 manager 테이블의 id 필드 constraint 수정  
ALTER TABLE MANAGER MODIFY COLUMN id BIGINT AUTO_INCREMENT;  
  
# 문제 3.INSERT를 사용하여 수강생들을 관리하는 manager 추가  
INSERT INTO MANAGER(name, student_code) VALUES('managerA', 's1');  
INSERT INTO MANAGER(name, student_code) VALUES('managerA', 's2');  
INSERT INTO MANAGER(name, student_code) VALUES('managerA', 's3');  
INSERT INTO MANAGER(name, student_code) VALUES('managerA', 's4');  
INSERT INTO MANAGER(name, student_code) VALUES('managerA', 's5');  
INSERT INTO MANAGER(name, student_code) VALUES('managerB', 's6');  
INSERT INTO MANAGER(name, student_code) VALUES('managerB', 's7');  
INSERT INTO MANAGER(name, student_code) VALUES('managerB', 's8');  
INSERT INTO MANAGER(name, student_code) VALUES('managerB', 's9');  
  
# 문제 4.JOIN를 사용하여 managerA가 관리하는 수강생들의 이름과 시험주차별 성적 추출  
SELECT a.name, a.exam_seq, a.score  
FROM (SELECT s.student_code, s.name, e.exam_seq, e.score  
FROM student s join exam e on s.student_code = e.student_code) a join manager m on a.student_code = m.student_code  
WHERE m.name = 'managerA';  
  
# 문제 5.STUDENT 테이블에서 수강생이 삭제될 경우 EXAM 테이블에서 해당 수강생의 성적과 MANAGER 테이블에서 관리하는 목록에서 자동 삭제