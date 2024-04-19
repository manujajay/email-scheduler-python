# Email Scheduler in Python

This README provides a guide on how to create an email scheduler using Python. It includes setting up your environment, writing the Python script to schedule emails, and using the `schedule` library to manage timing.

## Prerequisites

- Python environment
- `pip` for installing Python packages

## Setting Up Your Environment

1. **Install necessary Python packages:**
   ```bash
   pip install schedule smtplib
   ```

## Writing the Email Scheduler Script

1. **Create a Python script named `email_scheduler.py`:**
   - This script will use the SMTP protocol to send emails at scheduled times.

   ```python
   import smtplib
   from email.mime.text import MIMEText
   from email.mime.multipart import MIMEMultipart
   import schedule
   import time

   def send_email():
       sender_email = "your_email@example.com"
       receiver_email = "receiver_email@example.com"
       password = "your_password"

       message = MIMEMultipart()
       message["From"] = sender_email
       message["To"] = receiver_email
       message["Subject"] = "Scheduled Email Test"

       body = "This is a test email sent by Python. No need to reply."
       message.attach(MIMEText(body, "plain"))

       server = smtplib.SMTP('smtp.example.com', 587)
       server.starttls()
       server.login(sender_email, password)
       text = message.as_string()
       server.sendmail(sender_email, receiver_email, text)
       server.quit()

   # Schedule the email
   schedule.every().day.at("10:30").do(send_email)

   # Loop so that the scheduling task keeps running
   while True:
       schedule.run_pending()
       time.sleep(1)

   ```

## Running the Script

- Run the script using Python:
  ```bash
  python email_scheduler.py
  ```

## Conclusion

You've now successfully set up an email scheduler in Python. This script can be customized to send emails at different times or in response to various triggers.

For more detailed information on scheduling tasks in Python, visit the [schedule library documentation](https://schedule.readthedocs.io).
