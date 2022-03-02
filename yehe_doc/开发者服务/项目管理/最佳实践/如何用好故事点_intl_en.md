This document describes how to use story points in CODING.

## What Is a Story Point?

In traditional IT projects, the project manager often needs to estimate the costs for an upcoming project, including the workload, software and hardware costs. At the end of a project, most teams will find that the cost estimates that took a long time to prepare are often very different from the actual costs when reviewing the project. Traditional software teams usually estimate workload with time. Time is an **absolute value** that is usually estimated with historical empirical information. Time estimation works for teams with a fixed process and stable requirements. However, these meticulous estimates often restrict teams that are facing changing complexities. Every step of the way, a team has to check back with the original plan: Have we exceeded the estimated time? Are we up against the deadline? Have we achieved the original plan?

A core difference between agile estimation and traditional time estimation is the concept of **relative value**. Agile estimates are based on story points rather than absolute estimates in days or hours. Story points are a common **relative value** in agile development. In other words, given two requirements, we can estimate that one is larger than the other by a number of times, but we are unsure of the exact workload of each requirement.

## What Are the Benefits of Story Points?

- Team members often have an emotional attachment to dates, and relative estimation removes the emotional attachment.
- The workload estimate of each team differs slightly, meaning that their speed (in points) will differ.
- Once a consensus has been reached on the relative value (or difficulty) of a story point, the point can be assigned quickly without debate. 

**Story points allow teams to resolve problems based on difficulty rather than time. Team members can focus on creating value instead of the amount of time spent.**

In practice, estimation with time and story points each have their own advantages and disadvantages in different scenarios. In summary, good estimation practices help teams stay on top of project costs and profitability and reach a consensus on the effort, priority, and value of requirements to be delivered, leading to better business decisions. Let's take a look at how to estimate with story points.

## How to Use Story Points

### Prerequisites

Teams using story points should:

- Use fixed iteration durations (usually 2 weeks).
- Maintain a relatively stable team.

### Using story points for the first time

When using story points for the first time, a team should establish a benchmark by determining a previous requirement of equivalent effort to 1 story point.
For example, a "Create xxx page" function counts as 1 point. Accordingly, a "Modify xxx" function would also count as 1 point, and a simple search function would count as 2 points. In other words, the search function requires twice as much effort.

>? Story points are measured using the Fibonacci sequence: 1, 2, 3, 5, 8. (CODING uses an improved model.) In the approximate Fibonacci sequence, the difference between adjacent numbers increases as the numbers increase, allowing the difficulty of requirements to be easily identified and compared. For example, a 34-point requirement is different from a 21-point one, but it would not be very agile to debate over whether a feature is 34 or 35 points.

### Steps

Before a new iteration starts, all members need to meet to assess the story points of requirements.
![](https://main.qcloudimg.com/raw/3781e4675919f8b24d7c35e85a9db326.jpg)

Suppose the team has agile planning poker cards (each with a story point on the back).

- Each team member (except the product owner) picks a card of a certain color.
- The product owner describes a backlog item to be estimated and addresses questions from team members.
- The team discusses the backlog item.
- Each team member makes an estimate according to their judgment and puts the estimation result face down on the table.
- When all team members have completed their estimate, everyone reveals their card at the same time.
- If everyone has the same estimate or similar ones, the value is the consensus for the backlog item.
- If the difference in value is relatively large, the estimation results need to be discussed.
- Repeat the process above until a consensus is reached.
- The product owner selects the next backlog item to estimate.

The estimation results are put face down initially to avoid the herd effect (or deference to authority) that may result in random changes to one's result during the assessment.

### After an iteration

- At the iteration retrospective meeting, check the total number of completed story points and record them.
- Use the total number of points completed in the iteration as a reference to plan the next one. Usually, each iteration will have slightly more story points than those completed in the last iteration, so the team can gradually become more efficient.

## Conclusion

During actual agile development, the estimated number of points may be different from the actual situation due to business uncertainty, new changing factors, and subjective factors. We hope the following suggestions can help you improve story point estimation efficiency:

- **Involve all relevant members in the estimation.** With more comprehensive information comes more mature results. During the estimation process, team members can share their logic, experience, and hypotheses, creating synergy.
- **Reference previous work.** In the iteration retrospective, review and reflect on the accuracy of the estimate to improve the next iteration estimate.
- **Choose the right estimation method for story points.** Estimation methods differ for projects of different types and effort. Popular estimation methods include planning poker, T-shirt size, and dot vote.

