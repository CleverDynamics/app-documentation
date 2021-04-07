## 2.3.8

**Bug Fixes**

-   Interactions not saving

## 2.3.7

**Bug Fixes**

-   Status on Credit Released Orders - Release order from the Credit Held list,
    sets the Credit Status to "OK" It should set the Credit Status to "Credit
    Released". The filtered release list doesn’t show the orders that have been
    released, because its filtered to "Credit Released"

**Enhancements**

-   Reassign Credit controller - Once a Credit Controller has been assigned to a
    Customer there isn’t a way to reassign them to another credit controller

-   Customer Posting Group added to main page

## 2.3.6

**Bug Fixes**

-   Error renumbering customer record

## 2.3.5

**Bug Fixes**

-   Recalculate All / Recalculate Entries does not update customer status

## 2.3.4

**Bug Fixes**

-   Customer modify permission still required after fix in 2.3.2

## 2.3.3

**Bug Fixes**

-   Upgrade code missing permissions

## 2.3.2

**Enhancements**

-   Users entering sales orders no longer require Customer modify permissions

    -   The Account Status field on the customer record may be updated when an
        order is entered and released which previously required explicit modify
        permissions on the Customer table

    -   The Clever Credit permission set now includes Indirect modify permission
        to the customer table which is elevated by the account status
        calculation code

## 2.3.1

**Bug Fixes**

-   Rename query web service CredCtrlRemainAmt to CreditCtrlRemainAmtStatus
    (workaround for an issue upgrading BC SaaS tenants)

## 2.3.0

**Enhancements**

-   New action on setup page to perform calculation of Clever Credit statistics
    (rather than on installation of the app)

-   Ability to select different contacts on the interaction page

-   Call manual release methods in Release Sales Documents codeunit

-   Select/deselect highlighted entries on interaction subpage

-   Different interaction types - ability to select between them on the
    interaction page

    -   "Make Phone Call" label changed to "Create Interaction"

## 2.2.22

**Enhancements**

-   Dependency on Clever Dashboard app to provide dashboard measures and charts
    on role centres

-   New queries published as web services to support dashboard measures

-   Before/After events in Credit Mgt. - Release codeunit

-   Performance improvements to the calculation of Clever Credit statistics

## 2.2.21

**Bug Fixes**

-   Calculation of Selected Entries on Make Phone Call Page – issue when entries
    were being selected and unselected during an interaction. The totals are not
    being displayed on the header of the interaction card.

-   Style Credit Status on Sales Header.

    -   Call to SetCreditManagementStatusStyle is OnValidate of field "Credit
        Mgt. Status Style TMN" which is never called. Make this call from
        OnValidate of "Credit Status TMN".

    -   Set Style and StyleExpr properties on Sales Order page.

**Enhancements**

-   Cancelling Credit Check. User currently has no way of cancelling the request
    for the accounts dept to review the order. Add a new action that will allow
    the user to cancel the credit check while the status is still credit held.

## 2.2.20

**Bug Fixes**

-   Table IDs do not match error when clicking on Customer No. link in Stats
    FactBox.

**Enhancements**

-   On Before/ After Manual Release Events - Add events before/after manual
    release in the Credit Management codeunit to allow custom subscribers to
    override or extend the checks that are performed when an order is released.

-   Allow a custom subscriber to have a custom definition of

    -   Overdue Credit

    -   TotalOverCreditLimit

    -   Or just override the entire function to decide whether a particular
        order should be credit held or not

## 2.2.19

**Bug Fixes**

-   Creating an Interaction Hangs - When using "Make Phone Call" from the to-do
    list page.

## 2.2.18

**Bug Fixes**

-   Handle licenses for trials and licenses the same i.e. the definition for
    AppIsLicensed() should be the same irrespective of the type of license.

## 2.2.17

**Bug Fixes**

-   2.2.16 has two fields:

    -   "Company Registration No."

    -   "Company Registration No. TMN"

We cannot publish this version to AppSource with a field without the TMN suffix.
We will need to remove the first field and ForceSync when we upgrade.

## 2.2.16

**Enhancements**

-   Use Clever Config Licensing - Use new functions in Clever Config to acquire
    the license count.

**Bug Fixes**

-   The date is not valid - 0D due date - Handle customer ledger entries with
    blank due date when calculating overdue days

## 2.2.15

**Enhancements**

-   Add Company Registration No. to customer card

**Bug Fixes**

-   Handle field rename - Handle field rename for fields which were over 30 char
    before. Allow for upgrading from previous versions

## 2.2.14

**Enhancements**

-   Ability to Filter Credit Held List by Credit Controller - Add Credit
    Controller field to Credit Held list and make it available for users to
    filter on. Flowfield from Customer table? Field that is populated on
    validation of Bill-to Customer No?

**Bug Fixes**

-   Split the License check to check whether the app is licensed and secondly
    that the user is licensed. Changed license check when releasing/posting
    sales documents to only check if the app is licensed as users who are not
    credit controllers must be able to release documents.

-   Customer record cannot be deleted - Customer record cannot be deleted. The
    bug was fixed in credit management (objects), migrate the bug fix into the
    app.

-   Reset customer contact no on business relation change - When business
    relation customer is changed, reset the original customer record and assign
    the contact no against new customer.

## 2.2.13

**Enhancements**

-   Renumber into Clever Finance Range - Renumber into 9097029 - 9097128

-   Rework calling Customer Statement - MS are changing how the customer
    statement gets called. We need to copy in Clever Credit.

-   Calculating Account Status When Calculating Ledger Entries - Use the routine
    that recalculates ledger entries to update the customer's account status.
    The only way that a customer should need to have their status updating
    without any other trigger (releasing an order, inserting a detailed CLE) is
    when a ledger entry moves from the not due ageing bucket to the first due
    ageing bucket.

-   Recalculate Account Status When Grace Period Changes - Changing the grace
    period might change whether some invoices are considered overdue and
    therefore change the status of the customer account.

-   Use Events OnBefore/OnAfter Manual Reopen/Release - Replace page action
    subscriptions with subscriptions to the OnBefore/OnAfter **Manual**
    Reopen/Release events which are now available in the sales release codeunit.

-   Remove Service Password Permission - Remove Service Password permission in
    Clever Credit Setup table - it isn't required anymore and the Service
    Password table will be removed in a future version.

## 2.2.12

**Enhancements**

-   Clever Credit Page Filters - Set the filter on the Credit Controller page
    according to the following logic:

    -   If the current user is the default credit controller then show customers
        with a matching or blank credit controller code

    -   If the current user is not the default credit controller, filter to
        customers with a matching credit controller code

        -   If no customer records fall within the filter, then remove change
            the filter to show customers with a blank credit controller code.

-   Optionally Bypass Cust. Account Status Calculation - Especially for data
    migration scenarios. Otherwise the calls the CLE. Modify cause a calculation
    each time.

**Bug Fixes**

-   NA Build Failing - Reference to VAT Statements - Fix build for NA image -
    otherwise installation will fail for US and CA tenants.

-   Installing App Fails When CLEs with No. Customer No. are Present - Prevent
    the app from attempting to retrieve the customer record in this case. The
    immediate problem is for the v1 app - presumably when the it is attempting
    to calculate customer stats when the CLE archived data is restored - but
    this could cause a problem for any version of the app.

-   A CLE without a customer no. is valid e.g. when some data compression has
    been performed on the db.

## 2.2.11

**Enhancements**

-   An option has been added to the My Notifications page to optionally disable
    credit held notifications on sales documents.

**Bug Fixes**

-   Fix to update the account status on the bill-to customer

-   DD (Clever Document Delivery) integration using incorrect field. The actions
    Queue/Send email on the Clever Credit page, pass a RecRef of the current
    records to DD. Previously this page was based on the Customer record, since
    its source table is now the Credit Control Cust. Entry TMN

-   Update the actions to get the corresponding Customer entry first, and pass
    this to DD

## 2.2.10

**Bug Fixes**

-   Update the Account Status when changing the due date on the customer ledger
    entry, therefore if the dates are changed so an invoice is no longer overdue
    the status on the customer card is updated.

-   When an order has been released from credit held you can amend the order and
    users can re-release if the order value is below the original amount,
    however adding a line discount of 100% or an order value of zero means the
    order is credit held again. This has been changed so that zero value orders
    do not go through the credit hold process again and can be re-released.

## 2.2.9

**Enhancements**

-   Update Account Status on Sales Order Deletion - Customer account status
    should be recalculated when a sales order is deleted e.g. if the order took
    them over their credit limit and deleting that order takes them back under
    again.

**Bug Fixes**

-   Incorrect Date used for Credit calculation - We use the Document Date of the
    document to drive the credit calculation this should be changed to TODAY.

## 2.2.7

**Enhancements**

-   Credit Held Reason Priority - Change the order in which Credit Held Reasons
    are assigned to orders. Reasons in order of importance:

    -   Overdue (most important to show)

    -   Over Credit Limit

    -   Blocked

    -   Credit Hold All Documents (least important to show)

Progress Bar for Recalculate Functions – Add a progress bar to the Recalculate X
functions that are run On Open of the Clever Credit page.

-   Calculate account status of the sell-to customer no. on release of a sales
    document. Recalculate the status of the sell-to customer no. when a sales
    document is released. This is for the scenario where an outstanding order
    puts a customer over their credit limit.

**Bug Fixes**

-   SETFILTER on Hold Incorrect - Overdue Credit query uses a filter on the On
    Hold field

## 2.2.6

**Enhancements**

-   Add "Account Status" option/enum card. Add this field (non-editable) to the
    customer card and list and credit control pages. Add a function to calculate
    the value of this field - allow it to be overridden by a subscriber.

    -   Blank

    -   Overdue

    -   Over Credit Limit

    -   Blocked

## 2.2.5.1

**Enhancements**

-   Licensing from Setup Page - Allow the user to access the Clever Credit Setup
    page, even if their session is not licensed and add an action to open the
    license details page from there.

## 1.0.4

**Enhancements**

-   Add Credit Controller to Clever Credit Interaction - Add and populate Credit
    Controller Code field. Use that field to set the Credit Controller Code of
    To-Do entries.

-   Enforce Licensed No. of Credit Controllers - Licensing by the number of
    credit controllers seems a better way to manage a count of licenses for our
    app.

-   Event Subscribers - easier to read and more concise if the code was in the
    extension objects themselves (or calls from the extension objects to
    functions in codeunits, where appropriate).

-   Code Analysis - a tidy up to stop the repository throwing up warnings from
    the code analysis.

-   UI/UX Changes - Changes to the UI, promoted actions, captions etc.
    particularly around the Credit Held List and Manage Credit Status

**Bug Fixes**

-   Overflow Error Showing on Chart - Overflow error decimal to integer
    attempting to drilldown on average days to pay.

-   License details not visible - No way to get to licence details page from
    Clever Credit page.

-   FactBox on Customer Ledger Entries Shows Unrelated Interactions - Ensure
    that only interactions for the given ledger entry are shown in the FactBox.

-   Permissions Error on Opening Assisted Setup Page - A user who doesn't have
    our permission set assigned attempts to open the Assisted Setup page
    receives a permissions error that they don't have permission to read from a
    table in our range.

-   Overflow on Decimal -\> Int – occurs when displaying the chart on drilldown
    of Avg. Days to Pay for a customer

## 1.0.3

**Enhancements**

-   Descriptions on Interactions/To-Dos - make better use of the description
    field on interactions/to-dos to make it clearer why certain records have
    been created.

    -   Move To-Dos Description - Move the description field below the customer
        fields on the To-Do card and after the customer fields on the To-Do
        List. Also, show the To-Do Entry No. as the first column on the To-Do
        list page.

    -   Descriptions on Interactions - Add a description field to the
        interaction card - which should be editable. This description should
        carry through to the to-do when automatically creating a to-do because a
        next interaction date has been entered.

    -   If the description field is blank when the Next Interaction Date is
        populated, populate the description with the text "Follow up call from
        %1" where %1 is the date of this interaction.

    -   Description of To-Do’s Created from Promised Payment Date - When we
        automatically create a to-do by entering a promised payment date on a
        customer ledger entry, we should populate the description of that to-do
        with "Check promised payment has been received."

**Bug Fixes**

-   Credit Controller Code from User ID – when creating the Credit Control code
    ee take the first 10 characters and convert it to be the Code, if there’s
    more than one we remove the last character and add a number. After checking
    that a credit controller exists with the same code, copy the User ID and
    then make it 2 characters shorter.

## 1.0.2

**Enhancements**

-   License Details Page - Create new page to display the status of the licence,
    when the trial expires and give the option to set a new date for the expiry
    of the trial. Create a new codeunit that will be responsible for checking
    the status of the licence when certain actions are performed in the product,
    pop notifications to warn that the trial is about to expire etc.

**Bug Fixes**

-   Assigning Customers to Credit Controller – if you cancel the lookup dialog
    box without assigning any customers to the credit controller, all the
    customers in your customer list are assigned to the credit controller.

## 1.0.1

**Enhancements**

-   Assign Customers Action on Credit Controller List - Add a new action to the
    Credit Controller List page. Show the Customer List (filtered to customers
    who have a blank Credit Controller). If the OK button is used to close the
    page iterate through the selected customers and set the Credit Controller
    code on each of them.

-   Rework Select Column on Clever Credit Interaction - The current UX works
    nicely on the Windows client, but not on the web client.

-   Print Selected Invoices from Clever Credit Interaction Screen - Add action
    to print selected invoices from the **Make Phone Call** screen. This will
    allow the user to download a PDF of the invoices and send to the customer
    while they are on the phone to them.

-   Days to Pay Chart - Add a new chart to the Clever Credit Statistics page to
    show the trend of a customer's payments over time. Plot the number of days
    to pay each invoice against time as a line chart. This will allow the user
    to see at a glance the trend of customer payments over time.

-   View Credit Control Interactions from CLEs (Customer Ledger Entries) - From
    the CLEs page the user can see invoices on the account. Add a FactBox so
    that they can see any interactions that have been made with the customer
    where this invoice has been discussed.

-   Message on Passing Credit Check - Display a message when a document passes
    the credit check when initiated by the user from the action on the Sales
    Order.

-   Add Credit Mgt. Items to Relevant Role Centers - Add a navigation to the
    Accountant and Business Manager profiles.

-   Improvements made to the:

    -   Assisted setup pages – fields moved around, clearer labeling of fields
        and what setup is required.

    -   Credit Controller pages – clearer visibility of setup

    -   Sales Documents - highlight credit held documents, show necessary Clever
        Credit fields to carry out sales actions correctly.

-   DateFormula AssistEdits - Add assist edit functionality to dateformula
    fields that are added to the app. Dateformulas are not easy to work with at
    the best of times, let alone if we are assuming that the user does not have
    any Microsoft Dynamics 365 Business Central experience.

**Bug Fixes**

-   Customer Table is empty Error – this happens when a Credit Controller is
    linked to a current User, but no customers have bene assigned to the credit
    controller. If the user, then tries to open the Clever Credit Page it
    errors.

-   Do Not Calculate Days to Pay for Non-Invoice Cust. Ledger Entries- They are
    being calculated making the Clever credit statistics entries hard to read.

-   Credit Control Contact Lookup - The Credit Control Contact on the customer
    card should only lookup to person contacts that are related to the customer
    account. Currently is it showing all contacts.

## 1.0

**Enhancements**

-   Default Data – Providing a function to create some default data when the app
    is installed. This is to include Aging Bands & Default Credit Controller.

-   Notifications for JIT (Just in Time – prompt accordingly when setup needs to
    be done, rather than as soon as the App is installed) Setup.

    -   Notification to perform global setup when the app is first installed

    -   Link to open Credit Control page

    -   Notification to create some credit controllers when Credit Control page
        is opened.

-   Assisted Setup – Assisted setups have been created to help guide users
    through Clever Credit setup and creating Credit Controllers.

-   Populate Credit Controller Filter on the Clever Credit Page – if you are
    setup as a credit controller the Clever Credit list will filter customers to
    those you correspond to. If the current Credit Controller is the default
    credit controller show customer records that have a blank credit controller
    value.

-   Unassign Customers on Delete – Customer should be unassigned from a credit
    controller when they are deleted.

-   Refactor Codeunits - Change Clever Credit to be split into several smaller
    codeunits.
