# Adverse Event Explorer

Compare the side effects reported for different drugs, using the FDA's public adverse event database.

Pick up to four drugs and see their most reported side effects next to each other, or open one drug for its full profile and a chart of reports per year. The data comes from the FDA Adverse Event Reporting System (FAERS) through openFDA, the FDA's free public data service.

**[Try it live](https://aneelpaulus.github.io/adverse-event-explorer/)**

## What you can do

- Compare 2 to 4 drugs. Each side effect shows the share of each drug's reports that mention it.
- Open any drug for its total reports, busiest year, a yearly trend chart, and its top 25 side effects.
- Narrow the reports to a range of years.
- Download the comparison as a CSV file.
- Load a psychiatry example (ketamine, esketamine, sertraline) or an oncology antibody example (daratumumab, rituximab, elotuzumab).

## How to read the numbers

FAERS collects voluntary reports of *suspected* side effects from doctors, patients, and drug makers. A report means someone thought a drug might be involved. It does not prove the drug caused anything, and the database has no record of how many people took each drug without a problem.

So a "12%" next to nausea means 12% of that drug's reports mention nausea. It does not mean 12% of patients get nausea. Report counts also rise with how widely a drug is used, how much press it gets, and how sick the patients taking it are. Treat differences between drugs as questions worth looking into, not answers.

## Terms that are not side effects

Reporters often type the disease being treated into the side effect field. That is why raw FAERS lists show "plasma cell myeloma" near the top for myeloma drugs. Other common entries, like "off label use" or "drug ineffective," describe how a drug was used or whether it worked rather than a side effect.

The tool sets these aside in a separate, clearly labeled section instead of counting them:

- **Use and effectiveness terms** come from a fixed list (for example off label use, drug ineffective, dose omission, disease progression).
- **The condition being treated** is worked out per drug from openFDA's "reason for use" field. A condition counts when it appears in at least 5% of the drug's reports and is at least a third as common as the drug's top reason for use. The threshold matters because each report lists reasons for every medicine the patient took. Without it, hypertension (from blood pressure pills taken alongside sertraline) would be wrongly hidden as a side effect of esketamine.

The decision is made drug by drug. Sedation is a main reason ketamine is given, so it is marked that way for ketamine, but it still counts as a side effect for esketamine. The rule is automatic, so check any set-aside term that matters to you.

When a side effect appears in one drug's top 100 but not another's, the tool shows "not in top 100" with an upper bound instead of guessing a number.

## How it works

For each drug, the page sends three requests to openFDA:

1. Reports per day, which the page adds up into a total and a per-year trend.
2. The 100 most common side effect terms (MedDRA terms, the standard vocabulary reporters use) with their report counts.
3. The 100 most common reasons for use, which the page uses to spot the condition being treated.

A drug matches when any drug in the report lists it by active ingredient, generic name, or product name. That includes reports where it was a drug the patient was also taking, not only the suspected cause, which tends to make counts larger.

The tool runs in your browser with no server or account. Drug names go only to openFDA.

## Limitations

- Brand names may give different results than generic names. Use the generic name for the most complete count.
- Products that contain the drug alongside something else are counted too (for example, an under-the-skin version of an antibody mixed with another ingredient). Related but separate drugs are not: "ketamine" does not match "esketamine."
- openFDA updates every few months, so the latest year is usually incomplete.
- openFDA limits how many requests one visitor can make per minute and per day. Heavy use may need a free openFDA API key (a possible future option).

## Run your own copy

The whole tool is one file, `index.html`. To host it free on GitHub:

1. Create a new public repository and upload `index.html`, `README.md`, and `LICENSE`.
2. In the repository, open **Settings**, then **Pages**.
3. Under "Build and deployment," choose **Deploy from a branch**, select `main` and `/ (root)`, and save.
4. After a minute or two, the page shows your live link.

## Disclaimer

For research and education only. Not medical advice, and not a tool for making treatment decisions. Not affiliated with or endorsed by the FDA. openFDA's own terms say its data should be treated as unvalidated.

## License

MIT. See `LICENSE`.

Built by Aneel Paulus, MD, MS.
