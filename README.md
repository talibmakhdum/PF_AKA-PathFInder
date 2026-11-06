# PathFinder

> **A clearer path from student interests to informed career
> decisions.**

A student-first decision-support platform intended to help Indian
students make better-informed decisions about academic streams, careers,
entrance examinations and study-abroad options.

**Primary audience:** Class 10--12 students\
**Secondary audience:** Parents and families\
**Project proposal:** four month prototype \| **Proposed core stack:**
Java + MongoDB

------------------------------------------------------------------------

## 1. Aim

PathFinder aims to turn fragmented education and career information into
a guided decision process. It helps students assess their interests,
academic strengths, goals and practical constraints; explore suitable
career options; compare trade-offs; identify relevant entrance
examinations; and investigate study-abroad routes within a budget.

PathFinder is decision support. It is not a licensed career counsellor,
a psychometric diagnosis, an admission guarantee or a prediction of
future success.

## 2. About the Project

Students and families often have to make high-impact academic decisions
using information scattered across many websites and influenced by
social or family expectations. PathFinder proposes one connected student
journey:

1.  **Assess** interests, marks, budget and goals.
2.  **Match** the student with ranked career options and explanations.
3.  **Compare** course duration, costs, eligibility, trade-offs and
    alternatives.
4.  **Plan** relevant entrance examinations and preparation timelines.
5.  **Evaluate abroad** country options against academic fit and budget.

The proposed product is designed primarily for students in Classes
10--12, with parents as a secondary audience.

## 3. Why PathFinder?

The project proposal identifies four related problems:

-   **Social pressure:** family expectations and peer choices can
    dominate a student's own interests.
-   **Limited exposure:** students may not know what a career involves
    in day-to-day work.
-   **Scattered facts:** eligibility, examinations, costs and college
    options are distributed across different sources.
-   **Late realization:** a mismatch between a student and a chosen path
    may become clear only after years of study.

PathFinder is intended to bring these questions into one guided
workflow: *What suits me? Which examinations do I need? What can I
afford? Can I study abroad?*

## 4. What Is Different About the Approach?

This section describes the design choices documented in the proposal. It
is not a verified market comparison or a claim that no other product
offers similar functions.

-   **Connected decision journey:** assessment, career matching,
    comparison, exam planning and abroad exploration are designed as
    connected steps around one student profile.
-   **Explainable recommendations:** the proposal calls for visible
    match dimensions, reasons for fit and reasons for caution---not an
    unexplained score or black-box verdict.
-   **Practical constraints included:** marks, budget, study duration
    and goals are considered alongside interests.
-   **Transparent guardrail:** scores guide exploration; they do not
    decide a student's future.
-   **Curated, database-first content:** core guidance is intended to
    rely on reviewed career, exam and country information rather than
    depending on third-party developer APIs for every answer.
-   **Scope discipline:** the first version prioritizes a useful set of
    in-depth profiles and concise overviews rather than promising
    exhaustive coverage immediately.

## 5. Project Overview and Proposed Modules

### 5.1 Assessment Engine

-   A 30-question interest assessment based on six RIASEC dimensions.
-   Student academic profile, budget and goal constraints.
-   Explainable top-five career matches.

The six dimensions are **Realistic, Investigative, Artistic, Social,
Enterprising and Conventional**.

### 5.2 Career Explorer and Comparison

-   20 proposed in-depth career profiles.
-   40+ brief career overview cards.
-   Searchable career profiles.
-   Side-by-side comparison of two or three paths.

### 5.3 Exam Navigator

-   35+ proposed examination profiles across major categories.
-   Eligibility and examination-pattern summaries.
-   Preparation timelines, deadline flags and reminders.

### 5.4 Study-Abroad Guide

-   Proposed country guides for the **USA, UK, Canada, Australia and
    Germany**.
-   Budget-aware filtering.
-   Eligibility guidance.

**Scope note:** The proposal prioritizes core profiles first. Remaining
career paths are intended to receive concise overviews and links to
official sources. Counts above are proposal targets, not verified live
database totals.

## 6. Recommendation Method

The proposal describes a transparent, deterministic recommendation
approach:

1.  Build a student profile from 30 interest questions across the six
    RIASEC dimensions, together with marks, budget, study duration and
    goals.
2.  Compare the student profile with career profiles using **cosine
    similarity** and **weighted constraint filters**.
3.  Return the **top five matches**, a dimension breakdown, reasons for
    fit and reasons for caution.

The engineering playbook further requires the team to document input
scales, career-profile values, score combination, weights, constraints
and edge-case handling. It calls for tests covering equal, low, high,
missing, contradictory and out-of-range inputs, ties and zero vectors
where cosine similarity is used.

A match score must not be presented as a prediction of success or as a
professionally validated psychological assessment. When no strong match
exists, the system should show alternatives or invite the student to
review their preferences rather than inventing a precise-looking score.

## 7. Technology Stack

The project proposal identifies this stack:

  -----------------------------------------------------------------------
  Layer                   Proposed technology     Intended responsibility
  ----------------------- ----------------------- -----------------------
  Frontend                HTML5, Tailwind CSS     Pages, forms,
                          CDN, vanilla JavaScript responsive layout and
                                                  browser interaction

  Web/backend             Java Servlets, JSP      HTTP requests,
                                                  server-side validation,
                                                  authentication and page
                                                  responses

  Data                    MongoDB                 Career, examination and
                                                  student profile
                                                  documents

  Support                 Gson                    JSON handling

  Support                 Jakarta Mail            Email reminders
  -----------------------------------------------------------------------

The engineering playbook also identifies **Eclipse** as the default Java
IDE when required by the college project and **VS Code** for frontend
files and documentation. Maven is preferred for Java dependencies if
permitted by the college project.

**Version decision still requiring confirmation:** the team must agree
on the JDK and Tomcat versions together. The playbook notes that Tomcat
10.1 uses Jakarta Servlet 6.0 and Pages 3.1, requires Java 11 or later,
and uses `jakarta.*` imports. If the required environment is Tomcat 9 /
`javax.*`, that choice must be documented and the APIs must not be
mixed.

React, a local LLM, email automation and production hosting are
described as optional later additions---not prerequisites for the first
working workflow.

## 8. System Architecture

The documented request path is:

**Student browser → HTML form / JavaScript → HTTP request → Java Servlet
→ service / recommendation logic → repository / data access → MongoDB →
response / JSP → student browser**

### Layer responsibilities

-   **Browser/frontend:** renders the interface, collects form inputs
    and sends HTTP requests.
-   **Servlet/controller:** receives requests, validates inputs on the
    server and coordinates the response.
-   **Service/recommendation layer:** applies deterministic scoring and
    weighted constraints; produces ranked results and explanations.
-   **Repository/data-access layer:** reads and writes the relevant
    career, exam and student documents.
-   **MongoDB:** stores the curated profiles and application data.
-   **JSP/response layer:** renders or returns the result for the
    browser.

The engineering playbook explicitly advises against placing every
responsibility in one Servlet. Request handling, recommendation logic,
database access and page rendering should remain separate as the
application grows.

## 9. Project Documentation

The supplied team documents establish the following development and
documentation practices:

-   Keep the repository README as the authoritative setup and project
    guide.
-   Document prerequisites, exact versions, installation, run steps,
    configuration variable names, tests, known limitations and
    contribution workflow.
-   Keep secrets and actual credential values out of documentation and
    source control.
-   Track work using GitHub Issues and GitHub Projects, with Backlog,
    Ready, In Progress, In Review, Blocked and Done states.
-   Give each issue one owner, acceptance criteria, dependencies and a
    reviewer.
-   Use short-lived branches and pull requests; test and review changes
    before merging.
-   Record research claims with a claim ID, source URL, source
    authority, date checked, evidence, confidence/uncertainty, owner and
    next review date.
-   Record bugs with environment, preconditions, reproduction steps,
    expected and actual results, evidence and frequency.

### Local setup information still to be completed

The supplied PDFs do not provide a verified repository URL, exact
JDK/Tomcat/MongoDB versions, environment-variable names, database seed
procedure, build command or confirmed application run command. These
must be filled from the actual repository and tested environment before
this README is treated as a complete installation guide.

## 10. Security, Privacy and Content Integrity

The engineering playbook defines a baseline approach. These are
documented requirements, not evidence that every control is already
implemented.

-   Use fictitious test students until a privacy policy and
    data-handling approach are agreed.
-   Collect only information required for the feature; do not request
    passwords, identity numbers or unnecessary sensitive details in
    student guidance flows.
-   Keep credentials out of source code. Use local environment
    configuration and restrict database network access.
-   Validate inputs on the server; browser-side validation alone is
    insufficient.
-   Use safe database-driver APIs or parameterized queries. Do not
    construct database queries by concatenating user input.
-   Do not commit `.env` files, API keys, database credentials, build
    outputs or IDE-generated secrets.
-   Do not place sensitive student data in demo collections.
-   Use only traceable and appropriately reviewed content.
    Time-sensitive facts such as exam dates, eligibility, application
    windows and visa rules require an official source, a checked date
    and a next-review date.
-   Estimates such as fees, living costs and salary ranges must state
    geography, year, range and uncertainty.
-   Clearly distinguish stable facts, time-sensitive facts, estimates,
    user inputs and algorithm outputs.
-   AI-generated code or claims must be reviewed and verified; generated
    output is not proof of correctness.

A privacy policy, retention rules, access-control design and production
security review are not specified as completed deliverables in the
supplied PDFs.

## 11. Testing and Quality Approach

The team playbook requires normal, boundary, missing and invalid input
coverage. The recommendation flow should be tested for:

-   Equal interest ratings and low-differentiation profiles.
-   Missing academic inputs.
-   Out-of-range or malformed values.
-   Ties and zero vectors.
-   Contradictory constraints.
-   Budget mismatch and uncertain financial-aid assumptions.
-   No strong career match.
-   Outdated examination information.
-   Empty database results and database/configuration failures.

The proposed six-week release gate is reached only when a student can
submit assessment values, the server validates them, deterministic
recommendation logic returns a result, a small curated career dataset
has traceable sources, the browser explains the result and handles
empty/error states, the interface works on mobile widths, and another
team member can run the application using the README.

## 12. Roadmap and Future Enhancements

### Proposed six-month delivery plan

  -----------------------------------------------------------------------
  Month                   Milestone               Planned output
  ----------------------- ----------------------- -----------------------
  1                       Foundation              Project setup, MongoDB
                                                  connection, login,
                                                  student stage and
                                                  dashboard

  2                       Assessment              RIASEC quiz, academic
                                                  and constraint inputs,
                                                  first recommendation
                                                  output

  3                       Career explorer         First 10 in-depth
                                                  profiles, search and
                                                  career comparison

  4                       Exam navigator          25 exam profiles,
                                                  timeline generator and
                                                  conflict warnings

  5                       Abroad guidance         Five country guides,
                                                  eligibility calculator,
                                                  remaining profiles and
                                                  email reminders

  6                       Polish and demo         Testing, responsive UI,
                                                  dark mode, seed data,
                                                  documentation and
                                                  presentation
  -----------------------------------------------------------------------

### Future enhancements identified in the documents

-   Expand career coverage beyond the initial in-depth profiles.
-   Extend examination and country-guide coverage with regular source
    reviews.
-   Add email reminders and more complete notification workflows.
-   Improve dashboards and authentication after the core decision
    journey works.
-   Consider React, a local LLM, more advanced deployment or CI/CD only
    when justified by the working core product.

The engineering playbook explicitly says not to add an AI chat
counsellor, complex deployment, exhaustive career coverage, email
notifications, advanced authentication, dashboards or a study-abroad
calculator in parallel with the first vertical slice. Scope should be
reduced---not progress misreported---if a milestone slips.

## 13. Project Status

**Status based on the supplied documents: proposal and planned
prototype.**

The project pitch describes a proposed six-month prototype. The
onboarding guide and engineering playbook define team preparation,
learning tracks, architecture, workflow and target acceptance criteria.
These documents do not provide test reports, deployment evidence, a
verified feature inventory or proof that the proposed modules are
implemented.

Therefore: - **Documented:** product concept, intended audience,
proposed modules, scoring approach, proposed stack, architecture
direction, team workflow, security baseline and roadmap. - **Not
verified by these PDFs:** current build state, completed modules,
production readiness, deployed URL, live user data, test pass rate and
repository release status.

Update this section only after checking the current repository and
running the application.

## 14. Team and Contributions

The onboarding guide lists these team members:

  Member ID   Name      Role track documented in the Engineering Playbook
  ----------- --------- ----------------------------------------------------
  M1          Gulam     Java backend and web application
  M2          Ansh      Data layer, search and comparison
  M3          Aman      Frontend and browser interaction
  M4          Makhdum   Product, research, testing and implementation lead
  M5          Aryush    Beginner development and QA contribution track

These are the role tracks assigned to member IDs in the supplied team
materials. They are not a verified record of completed individual
contributions. Actual contributions should be recorded through reviewed
issues, pull requests, tests and merged work.

## 15. Sources and References

### Supplied project documents

-   `PathFinder_Project_Pitch.pdf` --- product problem, workflow,
    recommendation method, modules, proposed stack, six-month plan and
    demo journey.
-   `PathFinder_Team_Engineering_Playbook.pdf` --- architecture,
    security and content-integrity baseline, team workflow, testing,
    delivery gates and technical references.
-   `PathFinder_Team_Onboarding_Guide.pdf` --- member list, onboarding
    tasks, beginner learning path and contribution workflow.

### Technical and learning references named in the Engineering Playbook

-   Official Apache Tomcat documentation and version compatibility
    matrix.
-   Apache Maven guides.
-   MongoDB Java Sync Driver documentation and Java getting-started
    guide.
-   MongoDB University: *Using MongoDB with Java*.
-   JUnit 5 User Guide.
-   GitHub pricing, GitHub Skills: *Introduction to GitHub*, and GitHub
    Projects documentation.
-   Pro Git book.
-   MDN Learn Web Development.
-   Chrome DevTools documentation.
-   VS Code FAQ and official editor getting-started documentation.
-   Trello plan comparison, Notion pricing and Figma Starter overview
    for optional team tools.
-   The playbook also lists selected Hindi learning resources from
    CodeWithHarry, Thapa Technical, Smart Programming and Code with
    Technyyks.

The engineering playbook states that its official references were
checked for that edition on **27 October 2026** where current pages were
available. Links, API versions, free-plan terms and time-sensitive
guidance should be rechecked before use. The supplied pitch does not
provide a complete bibliography for every career, exam or country fact;
those facts must have their own source records in the application
content.

## 16. Licence

**Project licence: Not specified in the supplied documents.**

Do not assume that the repository is MIT, Apache-2.0, GPL or otherwise
open source. The repository owner/team must choose a licence, add the
corresponding `LICENSE` file and confirm rights for code, datasets,
images and other assets before public distribution.

The Engineering Playbook advises linking to original public video
courses rather than downloading or redistributing them without
permission. Tool and dependency licences must be checked against their
official terms.

## 17. Contribution Guidelines

1.  Check the issue board and select a task in **Ready**.
2.  Confirm its scope, acceptance criteria, dependencies, owner and
    reviewer.
3.  Create a short-lived branch from the agreed base branch. Use
    descriptive names such as `feature/42-assessment-form`,
    `fix/51-empty-score-validation` or `docs/16-local-setup`.
4.  Make the smallest complete change; do not mix unrelated edits.
5.  Run relevant checks and test at least one edge case.
6.  Inspect `git status` and `git diff`; never include credentials or
    generated build artefacts.
7.  Open a pull request, link the issue, explain the change and provide
    test evidence.
8.  Resolve review feedback and merge only after review and tests pass.
9.  Update documentation and close the issue only when acceptance
    criteria are met.

A task is complete when its acceptance criteria pass, the change is
reviewed and merged, and another team member can run or verify it.

## 18. Disclaimer

PathFinder is an educational exploration and decision-support prototype.
Its matches and information are intended to help students investigate
options---not to replace students' judgement, parents, teachers,
qualified counsellors, official examination authorities, universities or
immigration authorities. Eligibility, dates, fees, salary estimates,
visa rules and admission requirements can change. Users should verify
consequential and time-sensitive information with the relevant official
source.

------------------------------------------------------------------------

*README content compiled from the three supplied PathFinder PDFs.
Proposal targets, engineering requirements and verified implementation
status are intentionally kept distinct.*
