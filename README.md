# Saving Qualifying Loan as a CSV File

This repo contains the results of the module 2 challenge. The assignment is to add new features and enhancements to the loan qualifier application. Specifically, the added feature is the ability to save the qualifying loans to a CSV file.

As usability and interactivity are hallmarks of good software development, we use the Fire and Questionary libraries to add even more functionality to the loan qualifier application. Our initial loan qualifier application is a python command-line interface ("CLI") application that allows users to see qualifying loans from lenders quickly and easily. The application works by taking in a `daily_rate_sheet` of loan criteria from various loan providers, asking the user a number of questions to evaluate their loan eligibility, and then returning to them a list of qualifying loans.

We enhanced the application to allow a user to save the qualifying loans to a CSV file and be able to share the results as a spreadsheet. The application now has the following functionality when the user runs the qualifier using the loan qualifier CLI. If (A) there is a list of qualifying loans, the application prompts the user to either (1) save the results as a CSV file or (2) opt out of saving the file. If the user chooses to save results as a CSV file, the application then (3) prompts the user for a file path to save the file. Once a file path is choosen, then (4) the application saves the results as a CSV file according to the file path. However, if (B) no qualifying loans exist, then the program (1) notifies the user and (2) exits.

---
## Technologies

This project leverages python 3.7 with the following packages:

* [fire](https://github.com/google/python-fire) - For the command line interface, help page, and entrypoint.

* [questionary](https://github.com/tmbo/questionary) - For interactive user prompts and dialogs

---
## Installation Guide

Before running the application first install the following dependencies.

```python
  pip install fire
  pip install questionary
```
---
## Usage

To use the loan qualifier application simply clone the repository and run the **app.py** with:

```python
python app.py
```

Questionary is used to input the location via the CLI. The following steps were taken to make this change:

    * The hardcoded file path for the `daily_rate_sheet.csv`file was removed from the `load_bank_data()` function call.

    * Inside the `load_bank-data()` function, a Questionary prompt was added to get input from the user. In the line where the value for `csvpath` was set, the `file_path` variable was replaced with the following Questionary prompt: `questionary.text("Enter a file path to a rate-sheet (.csv):").ask()`

        The new function appears as follows:

        ```python
        def load_bank_data():
            """Ask for the file path to the latest banking data and load the CSV file.

            Returns:
                The bank data from the data rate sheet CSV file.
            """

        csvpath = questionary.text("Enter a file path to a rate-sheet (.csv):").ask()
        csvpath = Path(csvpath)

        return load_csv(csvpath)
        ```

4. When prompted for your CSV file path, enter `./data/daily_rate_sheet.csv`.

Now we can dynamically set the location of the `daily_rates_sheet.csv` file.

Upon launching the loan qualifier application you will be greeted with the following prompts.

![Loan Qualifier Prompts](Images/loan_qalifier.png)
---
## Contributors

Brought to you by ET Home Loans.

---
## License

MIT


#### Prompt the User for Loan Information

Next, you'll create a dialog in a new function named `get_applicant_info()` that will prompt the user for their loan information. Complete the following steps:

1. In `app.py`, in the `run()` function, remove the parameters for `credit_score`, `debt`, and `income`.

2. In the comment above where `credit_score` is defined, change the comment from `# **Set** the applicant's information` to `# **Get** the applicant's information`.

3. Remove all of the defined values for `credit_score`, `debt`, `income`,`loan_amount`, and `home_value`, and set all equal to a new function named `get_applicant_info()`.

    ```python
    # Get the applicant's information
    credit_score, debt, income, loan_amount, home_value = get_applicant_info()
    ```

This function will prompt the user via the command line for the applicant's information, then return it so that you can set the values for `credit_score`, `debt`, `income`,`loan_amount`, and `home_value`.

#### Get the Applicant's Information

Now you're ready to build the `get_applicant_info()` function to fetch all of the required applicant information for the loan qualifier. Complete the following steps:

1. Above the `find_qualifying_loans()` function, define the new `get_applicant_info()` function.

    > **Hint** Don't forget to include the `def` keyword.

2. Inside `get_applicant_info()`, set the `credit_score` variable using the Questionary `text()` syntax. Repeat this step for the `debt`, `income`, `loan_amount`, and `home_value` variables. Your code should look as follows:

      ```python
      credit_score = questionary.text("What's your credit score?").ask()
      ```

3. Right now, all values received through Questionary will be set to the type `string`, but the values must be set to `float` to perform floating-point arithmetic. So convert the credit score to `integer` and the rest of the values to `float`.

    Inside the `get_applicant_info()` function, below where you've created the variables using Questionary, convert the variables from strings to numeric values. Use the following syntax as a guide (the remaining variables will be floats):

    ```python
    credit_score = int(credit_score)
    debt = float(debt)
    ```

4. Inside the `get_applicant_info()` function, write the statement that will return all of the variables.

That was a lot of code! But you're almost done—just run the application to check your work.

#### Run the Application

Run your command-line-powered loan qualifier app to see what an amazing job you've done!