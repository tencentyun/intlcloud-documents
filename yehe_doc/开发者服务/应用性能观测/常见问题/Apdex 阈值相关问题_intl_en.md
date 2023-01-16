### What is Apdex?
Application Performance Index (Apdex) was developed by an alliance of companies to specify a uniform way for reporting and measuring the performance of applications. It averages your application score in the range of 0–1, indicating where the digital experience offered to your users falls in the satisfaction range. `0` indicates that no user is satisfied, while `1` indicates that all users are satisfied. This helps you better understand the user sanctification of your application.



### What is the rule of Apdex threshold calculation?
The metric has three response counts for an application:
- Satisfied: The response time is less than or equal to the Apdex threshold, indicating that the user will not be affected by the response time and will be efficient in operations.
- Tolerating: The response time is greater than the Apdex threshold and less than or equal to four times the threshold, indicating that the user will perceive but can tolerate the response time.
- Frustrated: The response time is greater than four times the Apdex threshold.



### What is the formula of Apdex threshold calculation?
Apdex = (number of satisfied users + number of tolerating users/2)/total number of samples
The metric is in the range of 0–1, subject to the response time of the application. `1` indicates that all users are satisfied with the application performance, `0` indicates that no user is satisfied, and `0.5` indicates that all users are tolerating.
