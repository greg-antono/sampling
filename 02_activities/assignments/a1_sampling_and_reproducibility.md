# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Greg Antono

```
In the Python script, a dataframe was created via a simulate_event function, representing 1000 individuals who attended events (200 from weddings and 800 from brunches). This list of 1000 individuals is the sampling frame.

The model involves multi-stage sampling. We first observe stratified random sampling in the form of the population being divided into two strata: weddings and brunches. The sample size is the subset of them being infected based on the ATTACK_RATE of 10%. This is a case of simple random sampling, whereby there is no replacement occuring (i.e., randomly infections to a fixed proportion of the sample frame, assuming that everyone has a uniform chance of being infected). Another example of simple random sampling comes from the first step of contact tracing, whereby the model randomly decides which infected people get traced (in the blogpost, the assumption was that contact tracing occured at a rate of 20%). In the next step involving secondary contact tracing, it is no longer probability sampling, as it is based on the prior sample from primary contact tracing: if two or more infections were traced to the same wedding/brunch (i.e., based on primary contact tracing), all individuals associated with that event would be tested. I would classify this as snowball sampling (since the two individuals "snowballed" into the testing of all other participants at the event).

Lastly, the code adds a final layer of sampling with repeated simulation. The generated graph from the original code reproduces the true proportion of wedding infections as shown in the blogpost, but doesn't reproduce the observed proportion of wedding infections. By modifying the code from 1000 to 100 and running it several times, the histograms are different on different runs, as new random samples are generated each time.

In order to make this reproducible, I've added a random seed within the function, which essentially ensures the same set of results (i.e., histogram outputs are the same( on every run, even though each trial obtains a different value of m.

```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 09/04/2025`
* The branch name for your repo should be: `assignment-1`
* What to submit for this assignment:
    * This markdown file (a1_sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `assignment-1`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
