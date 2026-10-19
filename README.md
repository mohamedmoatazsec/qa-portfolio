# Mohamed Moataz - software testing portfolio

mohamedmoatazsec@gmail.com | [LinkedIn](https://www.linkedin.com/in/mohamedmoatazsec)

## Review order

1. [01_Mohamed_Moataz_Project_Overview.pdf](01_Mohamed_Moataz_Project_Overview.pdf) - one-page project overview.
2. [02_Mohamed_Moataz_QA_Case_Study.pdf](02_Mohamed_Moataz_QA_Case_Study.pdf) - scope, cases, findings, API results and evidence details.
3. [Website cases](03_Web_Test_Cases.md) and [defect reports](04_Defect_Reports.md) - complete editable records.
4. [Postman collection](API/Live_DummyJSON.postman_collection.json) and [API cases](API/API_Test_Cases.md) - runnable requests and recorded outcomes.
5. `Evidence/` - original screenshots and timestamped execution records.

Recorded on 19 October 2026. Website checks used SauceDemo; API checks used DummyJSON as a separate exercise. The public SauceDemo `problem_user` account intentionally exposes the three reported defects. The portfolio covers the recorded scenarios, with seven baseline website checks passed and all 55 API assertions passed.

Execution method: browser-assisted functional checks; API assertions executed with Newman 6.2.3. Original environment details are preserved in the evidence records. Proposed defect priorities reflect impact within this case study.

## Reproduction

Website setup and inputs appear in each case. Use the site's published demo credentials and the supplied invented checkout data. For a clean cart, use the working `standard_user` account to remove any existing items before preparing the stated case setup.

For API testing, import the collection into Postman, keep `baseUrl` as `https://dummyjson.com`, use No Auth, and run one iteration. Clear existing host authentication cookies before API-10. Expected full-run result: 55 passing assertions.

`Manifest_SHA256.json` records integrity checks for the supplied files.

## Postman workspace run

The collection was imported into Mohamed Moataz's Postman workspace and run in the Postman web application on 19 October 2026 at 14:10 Cairo. One iteration completed with **55 assertions passed, zero failed and zero errors** across ten requests. Stored cookies were excluded for the unauthenticated negative case.

The [results screenshot](Evidence/Postman/Postman_Run_Results.png), [visible results](Evidence/Postman/Postman_Run_Visible_Results.txt), and [run record](Evidence/Postman/Postman_UI_Run.json) provide evidence of this additional run. The original Newman execution remains preserved separately.
