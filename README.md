# Incident report
Issue Description : Latency in working with order management console application 
Incident Priority : P2 
Impacted users : 10
Date and time issue reported : 6/1/2022 8 AM EST
Issue resolved by : 6/1/2022 8:45 AM EST
Caught by monitoring : Y
Impact detail : Order managemet console (OMC) home page is spinning for few users and they are unable to move forward with the application . This is not a widespread issue , as the applictaion is not entirely down and working as expected for few of the users .
Triage sequence : OMC support team got notified through monitoring alert which indicated that the response time reached the maximum threshold for OMC home page.
Upon checking the logs it was observed that one of the four OMC proudction nodes is down due to maximum space utilization and throwing OOM exceptions 
Worked with the windows server team and killed the instance of the node which was done and performed a recycle .
After the recycle, checked that the load balancing is properly done and the impacted node is taking the traffic . 
Checked if there are any impacted orders which are stuck during the downtime of the node and found there are none and communicated the same to the users .
Performed end to end validations on the OMC appliction and made sure there are no hiccups in the performance and everything is working as expected.
Sent an all clear email to business with the impact details .
RCA : Support team found that there was a batch job running overnight on the impacted node which was supposed to end by 6 AM EST, and that caused overload on the node and making it throw OOM exceptions. The failure in the batch is due to the incorrect details entered by the user and instead of terminating , it got stuck in a loop .
Preventive measures : Support team needs to make sure that there are no active batches running which are not supposed to during the start of the business hours .
Set monitoring alarms for batch job failures.
Teams joined in the call : OMC support , Windows , Enterprise support desk. 
