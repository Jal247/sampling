# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Jalpa Purohit

```
Please write your explanation here...

```
1. Population:

Sampling Frame: The sampling frame is all individuals attending events (weddings and brunches), represented in the ppl DataFrame. Specifically, 200 individuals are assigned to the "wedding" event, and 800 individuals are assigned to the "brunch" event. 

Population size is 1000

Population Setup: The population is split between these two types of events, and each individual is initially marked as not infected ('infected': False) and not traced ('traced': np.nan).

The sampling process in this model includes:

1. Initial Infection Sampling(Primary Sampling): Randomly selecting infected individuals based on an attack rate.

   Sampling Procedure: A subset of individuals is randomly selected to be infected based on the    attack rate of 10%. 

   In this case, the sample size is 10% of the total population (1000 individuals) which is 100 individuals.

    Sampling Distribution: The selection of infected individuals follows a uniform distribution because each individual has an equal probability of being infected.

    Underlying Distribution: This step involves simple random sampling without replacement, where the number of infected individuals is proportional to the population size and controlled by the attack rate.

2. Secondary sampling: Tracing Infected individuals.
Primary Tracing: Tracing infected individuals using a Bernoulli distribution with a success rate.

    Sampling Procedure: Once individuals are infected, a random process determines whether they are traced. with the traced success rate 20%

    So, here Population size is 100. 

    Sample Size: The number of infected individuals that are traced is dependent on the trace success rate (20%, defined by TRACE_SUCCESS = 0.20). For each infected individual, there is a 20% chance they are traced. 
    So, we can say that sample size will be 20 individuals.

    Sampling Distribution: The sampling follows a Bernoulli distribution for each infected individual (each individual is either traced or not based on a success rate of 0.20).

    Sampling Frame: The sampling frame for this stage is limited to the subset of individuals who are infected.

3. 3rd Sampling:Tracing Based on Event Attendance

Secondary Tracing: The secondary tracing operates as a threshold-based rule. The proportions of infections and traces attributed to each event type (weddings vs. brunches) are then calculated to assess the impact of contact tracing.

Sampling Procedure: The sampled individuals are those who are both infected and attended events that met the threshold for secondary tracing. (SECONDARY_TRACE_THRESHOLD = 2)

Sampling Frame: The sampling frame for this secondary tracing includes the set of individuals who are infected and whose event type has passed the secondary trace threshold. Specifically, events with at least 2 traced individuals.

Underlying Distribution: This step is a condition based or rule applied to the events with a sufficient number of primary traces.

5. Outcome Calculation

Proportion Calculation: Finally, the model calculates the proportion of infections and traced cases that can be attributed to weddings. 

6. Simulation

Repetition: The entire simulation process (from event creation to infection and tracing) is repeated 50,000 times:

This allows the model to generate a distribution of outcomes (proportions of infections and traces) to be analyzed in aggregate.




## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
