#Readme
Issue Summary

Duration of Outage: August 10, 2024, 10:00 AM - 12:30 PM EAT

Impact: During the outage, the SokoBeauty platform experienced severe performance degradation, leading to complete unavailability of the booking service. Users were unable to book salon services, with 85% of the user base affected. Users experienced timeouts, slow loading times, and errors when attempting to access the booking page.

Root Cause: The root cause of the outage was an unoptimized database query introduced during a recent update, leading to a massive spike in CPU usage and exhausting server resources.

Timeline

10:05 AM: Issue detected by automated monitoring system due to a sudden spike in CPU usage on the primary database server.
10:10 AM: Incident escalated to the on-call engineer after the monitoring alert was triggered.
10:20 AM: Initial investigation began; engineers assumed a hardware failure on the database server due to high CPU usage.
10:35 AM: Database logs and metrics were analyzed, revealing multiple slow queries, but the cause was not immediately clear.
10:50 AM: Engineers focused on the database configuration, suspecting a misconfiguration of the caching system.
11:10 AM: Realized that the recent code deployment might be the cause; rolled back the update to see if performance would improve.
11:30 AM: Performance slightly improved, but the root cause was still not identified.
11:45 AM: A thorough review of the latest code changes identified an unoptimized SQL query in the booking service.
12:00 PM: A hotfix was deployed to optimize the query.
12:30 PM: Service fully restored, with normal CPU usage and booking functionality confirmed.

Root Cause and Resolution

The root cause of the outage was an unoptimized SQL query introduced in a recent update. The query involved multiple joins and lacked proper indexing, leading to high CPU utilization on the database server. This caused significant performance degradation across the entire platform, particularly affecting the booking service, as it relied heavily on this query.

To resolve the issue, the engineering team rolled back the recent update to temporarily alleviate the performance problems. A hotfix was then developed, which optimized the problematic SQL query by adding necessary indexes and restructuring the query logic to reduce the computational load. The fix was deployed, and the system performance returned to normal.

Corrective and Preventative Measures

Improvements/Fixes:
- Improve the code review process to include performance impact analysis for database queries.
- Enhance monitoring and alerting to detect inefficient queries and database performance issues earlier.
- Implement load testing in the staging environment to simulate the impact of new queries before production deployment.

Tasks:
1. Patch Nginx server: Ensure the server is running the latest stable version to prevent similar performance issues.
2. Add monitoring on server memory: Implement detailed monitoring of memory usage to detect potential resource exhaustion early.
3. Conduct a database audit: Review current database schemas and queries to identify and optimize other potential performance bottlenecks.
4. Update deployment checklist: Include performance testing and database query analysis in the deployment checklist to catch issues before they impact production.
5. Improve rollback procedures: Develop automated scripts for quicker rollbacks in case of emergency, reducing downtime.

This postmortem highlights the importance of thorough testing and performance analysis during the development cycle. By implementing the corrective measures outlined above, we aim to prevent similar incidents in the future and ensure a stable and responsive platform for all SokoBeauty users.


