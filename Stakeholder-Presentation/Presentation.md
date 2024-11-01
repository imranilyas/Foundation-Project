# Presentation to Stakeholders

## Goals of the Current Iteration of the Project
The MVP of this Sprint was to create test case documentation and add said documentation onto Jira along with
the test cases and defect reports.

Stretch goals were to perform extra Error Guess Testing and Non-functional System testing. In future iterations, I plan
to hit those goals.

## Present Test Summary Report
I had 36 different tests across 13 test cases in Jira. All the todo portions / Not in Cycle
coverage refer to the defect reports that were added during text execution. Testing was peformed
through the use of multiple black box techniques of Acceptance Testing. This includes:
- Boundary Value Analysis
- Error Guess Testing
- Dynamic Testing i.e. Positive and Negative testing
- Equivalence Partition Testing

A majority of use-cases failed according to the middle graph. In fact, more would fail but I took an isolated approach
with some of the testing. As you can see, I found myself labeling a majority of the defects as High or Medium priority.
I felt the defects in this application either disrupted functionality or had high security risks with the user's data.

One of the most severe defects that I came across was planets being removed from other accounts by other users.

## Showcase Acceptance Testing Summary Report
My acceptance testing report for the use-cases is mostly just an extension of the tests that were created on Jira.
While they may not look as polished, the real beauty is in my alternative way of Acceptance Testing. I played the role
of an end-user and went screen by screen in order to get in the mind of a user of the Planetarium application. 

The most interesting defect or maybe feature if you are so inclined is the defect when adding an image for your moon or
planet. While acting as an end-user, I tried to use a .png file and the application gave me an Invalid File Error in the
console.

## Mini-Sprint Retrospective
The RTM and Test Planning went well in the Sprint. However, I severely underestimated the Test Case phase of the STLC.
Also, organization was a headache and I found out that I would need to contact admin to delete User Stories and Issues. 
This is likely a "Role" feature on Jira, so I'll have to look more into it later. Phase 3 caused me to fall behind on
the schedule the most.

Now that I know how to organize my data in a more appropriate fashion, the next sprint or future projects using the STLC
should be smoother. Next sprint, I would like to investigate more into Exploratory Testing, more specifically in how
moons are being used throughout the application. They appear to be global and I'm curious to find out whether it is 
a frontend issue or something in the database that needs correcting.