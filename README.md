# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. latency in getting the recent value from the server
3. Mismatch in saving data in csv file due to server issues, continuity of 30 mins record could be disturbed
4. error in PDF generation to export data from the server
5. false alarm/ notifications


### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter |  Yes          | This would be much reliable and trusted
Counting the breaches       |  Yes          | This is part of the software being developed
Detecting trends            |  Yes          | This function is being developed
Notification utility        |  Yes          | This function is developed to notify the latest report/utility availability

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write the attribute of BMS into the PDF when it has crossed the threshold level/breach
4. Write the number of breach of an attribute in to the PDF that has occured for a that weak
5. write the recordings into the PDF when a breach occurs or remains same for 30 mins
6. Write the server under maintainance or unavailability log into PDF when the server is down or unaccessible
7. Check the data is written into PDF is as in csv
8. Check and alert that the report is generated every week
9. check if the notifications are triggered when the PDF is generated
10. Check the PDF is not currupt and file extension is appopriate
11. Check the data is corrupt that is collected in csv file


(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input                      | Output                          | Faked/mocked part
|--------------------------|--------------              |---------------------------------|---
Read input from server     | csv file                   | internal data-structure         | Fake the server store
Validate input             | csv data                   | valid / invalid                 | None - it's a pure function
Notify report availability |PDF file                    | alert/notofication if available | fake- the notification of availability of report
Report inaccessible server | request to server data     | accessible status to PDF file   | Fake - the status 
Find minimum and maximum   |csv file                    | PDF file                        | None - it's a pure function
Detect trend               | csv file                   | PDF file                        | None - it's a pure function
Write to PDF               | data buffer to read        |  PDF file                       |fake- the PDF generator
