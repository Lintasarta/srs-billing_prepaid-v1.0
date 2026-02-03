# System Architecture and Workflow

This section describes the high-level operational flow of the Prepaid Billing System.

1. **Onboarding and Initial Deposit:**
   - A new user signs up on the Service Portal and their account is automatically configured as "Prepaid".
   - To activate the ability to create services, the user must make an initial minimum deposit amount calculated with the formula: ((estimated full usage in 1 month) / 30) * 10, which represents 10 days of estimated usage.
   - Upon successful payment confirmation from the payment gateway, the deposit amount is credited to the user's organization balance.
   - The system generates and sends an invoice for the deposit to the user's registered email.

2. **Service Provisioning and Balance Check:**
   - When a user attempts to create a new service (e.g., an Instance, Storage), the system calculates the estimated cost for the minimum billing period (e.g., one hour for PPU).
   - It validates that the user's current deposit balance is sufficient to cover this initial cost. If the balance is insufficient, the user is prompted to top up their deposit.
   - If the balance is sufficient, the service is provisioned. The price of the service is recorded at the time of creation and is not affected by subsequent price changes made by a Superadmin.

3. **Usage Tracking and Daily Cost Estimation:**
   - The system continuously tracks the usage of all active services for each customer.
   - The Service Portal provides a "Daily Cost" or "Estimated Daily Charging" view, which gives the user a running estimate of their daily spending based on active services. This helps users predict the amount that will be debited from their deposit.

4. **Automated Daily Debit Process:**
   - A scheduled process (e.g., a cron job) is triggered every day at 08:00 (GMT+7).
   - This process calculates the actual charges for each active service over the preceding 24-hour period based on its billing type (PPU, Monthly, etc.).
   - The total calculated amount is then debited from the user's deposit balance. A record of this daily debit is stored for historical reporting.

5. **Prepaid Dunning Process**
   - Low Balance Reminder: If the customer's remaining balance is not sufficient for 10 days of estimated usage, a reminder is sent to the customer.
   - Service Suspension: If the customer's remaining balance is not sufficient for one day of estimated usage, the system will automatically suspend services. Information about the suspension is received by the customer.
   - Release Suspension: If the customer adds balance after suspension, the system will release the suspend status. Information about the successful balance top-up is received by the customer.
   - Resource Termination: If there is no additional balance added 30 days after the suspension date, the system will proceed to terminate the customer's resources.
   - Account Termination: If there is no additional balance added 60 days after the suspension date, the system will proceed to terminate the customer's account.

6. **Monthly Reporting:**
   - On the first day of each new month, the system generates a "Monthly Summary" for the previous month.
   - This summary provides a detailed breakdown of all services used, total consumption, and all daily debits that occurred during that month. This summary is accessible to the user via the Service Portal and can be downloaded.
