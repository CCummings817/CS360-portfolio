# CS-360 Mobile Architecture and Programming: Sightline Inventory App

**Briefly summarize the requirements and goals of the app you developed. What user needs was this app designed to address?**

Sightline is an Android inventory tracking app built for warehouse and job site use. The requirements were a working login with account creation, a persistent SQLite database that displays items in a grid, full create, read, update, and delete actions, and an SMS alert when an item runs out. The user need behind it comes from my work as an electrician apprentice: crews often don't know a material is gone until someone goes looking for it, which costs time on the job. Sightline gives users a quick, reliable count and a text the moment anything hits zero.

**What screens and features were necessary to support user needs and produce a user-centered UI for the app? How did your UI designs keep users in mind? Why were your designs successful?**

The app needed four screens: login with account creation, the inventory grid, an Add Item form, and an SMS alerts settings screen. I designed with a busy user in mind, so the plus and minus buttons sit right on each row, out-of-stock counts turn red, tapping a row opens a quick edit dialog, and an empty grid tells the user exactly what to do next. I used a charcoal and safety yellow theme that fits the trades and stays readable in bright light. The designs worked because every element connects to a real task, and the most common action, adjusting a count, takes a single tap.

**How did you approach the process of coding your app? What techniques or strategies did you use? How could those techniques or strategies be applied in the future?**

I built the app in layers, starting with the database, then login, then the grid actions, and finally SMS, and I ran each piece before moving to the next. I kept classes focused on one job: a DatabaseHelper for all SQLite work, a PasswordHasher so passwords are stored as salted hashes instead of plain text, an InputValidator for shared input rules, and an SmsAlertHelper for permissions and texting. The grid adapter only handles display and passes user actions back to the activity through a listener. I also used parameterized queries to prevent SQL injection and try-with-resources to close database cursors. This approach of small, focused classes and building in layers will carry over to any project, especially the larger field app I plan to build for the trades.

**How did you test to ensure your code was functional? Why is this process important, and what did it reveal?**

I tested in the Android Emulator after every major change, and I tested the unhappy paths as well as the happy ones: blank fields, wrong passwords, duplicate usernames, and a user denying SMS permission. I also closed the app completely and reopened it to confirm the data persisted. Testing matters because users will always find the paths a developer didn't think about. It revealed some real issues, like new class files landing in a generated build folder that would have been wiped on rebuild, and it showed me that the emulator needs its full phone number (15555215554) to receive a test text.

**Consider the full app design and development process from initial planning to finalization. Where did you have to innovate to overcome a challenge?**

The biggest challenge was SMS. The app had to keep working fully if a user denied permission, without crashing or nagging, so alerts are skipped quietly unless permission is granted and a phone number is saved. While writing my launch plan, I also found that Google Play restricts the SEND_SMS permission to apps that are the default texting app. Instead of ignoring that, I planned a production path that replaces direct SMS with push notifications so the app could actually be published.

**In what specific component of your mobile app were you particularly successful in demonstrating your knowledge, skills, and experience?**

I'm most proud of the out-of-stock alert flow, because it ties the whole app together. It uses the database, respects the user's permission choice, saves the user's alert number, and only fires when an item goes from having stock to zero, so users aren't spammed. It reflects both my technical growth in this course and my real-world understanding of what the people using this app actually need.
