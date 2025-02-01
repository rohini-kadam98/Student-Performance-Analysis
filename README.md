# Student-Performance-Analysis
## About Dataset
This dataset provides a comprehensive overview of various factors affecting student performance in exams. It includes information on study habits, attendance, parental involvement, and other aspects influencing academic success. The specific individual datasets at hand can be obtained at this link below: [Kaggle](https://www.kaggle.com/datasets/lainguyn123/student-performance-factors)
### Column Descriptions
Hours_Studied :	Number of hours spent studying per week.                                       
Attendance :	Percentage of classes attended.                                                       
Parental_Involvement :	Level of parental involvement in the student's education (Low, Medium, High).                                               
Access_to_Resources: Availability of educational resources (Low, Medium, High).                                     
Extracurricular_Activities :	Participation in extracurricular activities (Yes, No).                            
Sleep_Hours :	Average number of hours of sleep per night.                                   
Previous_Scores :	Scores from previous exams.                                                     
Motivation_Level :	Student's level of motivation (Low, Medium, High).                                                    
Internet_Access :	Availability of internet access (Yes, No).                                                         
Tutoring_Sessions	:Number of tutoring sessions attended per month.                                                      
Family_Income :	Family income level (Low, Medium, High).                                                         
Teacher_Quality :	Quality of the teachers (Low, Medium, High).                                                  
School_Type	: Type of school attended (Public, Private).                                                    
Peer_Influence :	Influence of peers on academic performance (Positive, Neutral, Negative).                                               
Physical_Activity :	Average number of hours of physical activity per week.                                                      
Learning_Disabilities :	Presence of learning disabilities (Yes, No).                                                                             
Parental_Education_Level :	Highest education level of parents (High School, College, Postgraduate).                                                                 
Distance_from_Home : Distance from home to school (Near, Moderate, Far).                                                      
Gender: Gender of the student (Male, Female).                                                   
Exam_Score :Final exam score.                                               

### Questions
1.Find the total number of students in the dataset.                                        
2.Calculate the average exam score of all students.                                         
3.Retrieve the highest and lowest exam scores.                                                
4.Find the number of students who have access to the internet.                                    
5.Find the average exam score based on school type (Public vs. Private).                                             
6.Check how many students participate in extracurricular activities and their average exvam scores.                                                         
7.Find the correlation between hours studied and exam scores by grouping students into study-hour ranges.                                                              
8.Analyze how parental education level impacts student performance.                                                            
9. Find the top 5 factors affecting exam scores using a correlation approach (ranking by average scores).                                                    
10.Identify the top 5 students who studied the most hours and their corresponding exam scores.                                                                     
11. Determine whether students who receive tutoring sessions perform better than those who don’t.                                                               
12. Find the relationship between sleep hours and exam performance.                                                     

### Tools Used:
1.MySQL
2.Power BI

### Analyze
#1.Find the total number of students in the dataset.                                                            
SELECT COUNT(*) AS Total_Students FROM student.StudentPerformanceFactors;                                                

#2.Calculate the average exam score of all students.                                
SELECT AVG(Exam_Score) AS Average_Exam_Score FROM student.StudentPerformanceFactors;                                  

#3.Retrieve the highest and lowest exam scores.                              
SELECT MAX(Exam_Score) AS Highest_Score, MIN(Exam_Score) AS Lowest_Score FROM student.StudentPerformanceFactors;                                  

#4.Find the number of students who have access to the internet.                                 
SELECT Internet_Access, COUNT(*) AS Count FROM student.StudentPerformanceFactors WHERE Internet_Access = 'Yes';                                   

#5.Find the average exam score based on school type (Public vs. Private).                                      
SELECT School_Type, AVG(Exam_Score) AS Avg_Score                                           
FROM student.StudentPerformanceFactors                                            
GROUP BY School_Type;                                                      

#6.Check how many students participate in extracurricular activities and their average exam scores.                                           
SELECT Extracurricular_Activities, COUNT(*) AS Student_Count, AVG(Exam_Score) AS Avg_Score                                     
FROM student.StudentPerformanceFactors                                          
GROUP BY Extracurricular_Activities;                                         

#7.Find the correlation between hours studied and exam scores by grouping students into study-hour ranges.
SELECT                                                
    CASE                                          
        WHEN Hours_Studied < 10 THEN '0-10 Hours'                                  
        WHEN Hours_Studied BETWEEN 10 AND 20 THEN '10-20 Hours'                                 
        WHEN Hours_Studied BETWEEN 21 AND 30 THEN '21-30 Hours'                            
        ELSE '30+ Hours'                                       
    END AS Study_Range,                                                         
    COUNT(*) AS Student_Count,                                                      
    AVG(Exam_Score) AS Avg_Score                                 
FROM student.StudentPerformanceFactors                                       
GROUP BY Study_Range;                            

#8.Analyze how parental education level impacts student performance                          
SELECT Parental_Education_Level, COUNT(*) AS Student_Count, AVG(Exam_Score) AS Avg_Score                                  
FROM student.StudentPerformanceFactors                                       
WHERE Parental_Education_Level IS NOT NULL                                            
GROUP BY Parental_Education_Level                                                   
ORDER BY Avg_Score DESC;                                          

#9. Find the top 5 factors affecting exam scores using a correlation approach (ranking by average scores).
SELECT                                                 
    CASE                                           
        WHEN Attendance > 90 THEN 'High Attendance'                                 
        WHEN Attendance BETWEEN 70 AND 90 THEN 'Moderate Attendance'                                    
        ELSE 'Low Attendance'                               
    END AS Attendance_Group,                                         
    Motivation_Level, Access_to_Resources, Sleep_Hours, Peer_Influence,                                    
    AVG(Exam_Score) AS Avg_Score                                       
FROM student.StudentPerformanceFactors                                       
GROUP BY Attendance_Group, Motivation_Level, Access_to_Resources, Sleep_Hours, Peer_Influence                            
ORDER BY Avg_Score DESC                                        
LIMIT 5;                                 

#10.Identify the top 5 students who studied the most hours and their corresponding exam scores.
SELECT Hours_Studied, Exam_Score                                  
FROM student.StudentPerformanceFactors                               
ORDER BY Hours_Studied DESC                                  
LIMIT 5;                                    

#11. Determine whether students who receive tutoring sessions perform better than those who don’t.                              
SELECT                                
    CASE                              
        WHEN Tutoring_Sessions = 0 THEN 'No Tutoring'                       
        ELSE 'Received Tutoring'                           
    END AS Tutoring_Status,                             
    COUNT(*) AS Student_Count,                               
    AVG(Exam_Score) AS Avg_Score                                          
FROM student.StudentPerformanceFactors                          
GROUP BY Tutoring_Status                            
ORDER BY Avg_Score DESC;                                        

#12. Find the relationship between sleep hours and exam performance.                                
SELECT Sleep_Hours, AVG(Exam_Score) AS Avg_Score                                  
FROM student.StudentPerformanceFactors                           
GROUP BY Sleep_Hours                               
ORDER BY Sleep_Hours;                                         

### Share
[Student Performance](https://github.com/rohini-kadam98/Student-Performance-Analysis/blob/main/student%20performance.pdf)

### Insights
1.Most students (6108 out of 6607) have internet access, which may influence their performance.                             
2.The average exam score is 67.24, with scores ranging from 55 to 101.                          
3.Students with highly educated parents tend to score higher.                              
4.Studying 10-30 hours per week yields better performance, while 30+ hours doesn’t show significant improvement.                                    
5.Balanced sleep (6-9 hours) is linked to better academic performance.                                       
6.High attendance and high motivation lead to higher scores.                                    
7.Positive peer influence results in higher average scores (81.50), while negative influence lowers them (73-74).                               
8.Students who receive tutoring perform better than those who don’t.                                         
9.Participation in extracurricular activities is associated with higher exam scores.                                       
10.School type impacts student performance, with some schools seeing an increase while others see a decline.                                               
### Recommendation
Encourage 10-30 hours of study per week for optimal performance.                         
Promote 6-9 hours of sleep to improve academic outcomes.                               
Boost student motivation and attendance through mentorship and rewards.                          
Provide tutoring programs to enhance learning and scores.                           
Foster positive peer influence and parental involvement for better results.                                               
