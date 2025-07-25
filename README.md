
# Logbook – Android Car Sharing App with AI OCR and SQLite

#### Video Demo:  [URL HERE](https://www.youtube.com/watch?v=k-yl5ljBSEs&ab_channel=MartinHild)

#### Code:
📂 [Java Source Files](./app/src/main/java/com/example/sqltest)

📂 [Layout xml Files](./app/src/main/res/layout)



by Martin Hild



### Description:


As a final project, I decided to develop my first own app - an Android app for car sharing. My idea was that multiple drivers sharing a car could enter the distance, date, and time of their drive. This way, it's easy to see who drove a shared car, when, and how far. The distance traveled is calculated using the car's mileage at the start and stop.

Additionally, I set three goals beforehand:

- Optical Character Recognition (OCR), so users wouldn't have to manually input the car's mileage but could scan it using their phone's camera.
- The captured data should be stored in a database.
- To make input more user-friendly, users could input date and time manually or through graphical elements (calendar and clock). By default, the current time and date are set but can be changed.


### Design choices:

**IDE:**

After some research, I learned that Android Studio is the official Integrated Development Environment for Android app development.

**Programming Language:**

I read in several forums that Java and Kotlin seemed to be well suited for my purposes. Since I had taken a Java course years ago, I decided to go with Java.

**OCR:**

I discovered [ML Kit](https://developers.google.com/ml-kit/vision/text-recognition/v2/android) and decided to use it for my Optical Character Recognition.

**Database:**

When it came to the database, I chose SQLite. Firstly, because I was already familiar with it from the CS50 course, and secondly, because I learned that SQLite was the most common database technology associated with Android applications due to its inclusion in the Android SDK.


### App Structure:

In Android Studio, an Activity represents a screen with a user interface. In my application activities are defined in Java classes but have additional functionality and lifecycle management specific to Android. Activities are associated with user interface layouts defined in XML files. The app also uses Java classes that are not Activities to organize the code and encapsulate logic.

**My app consists of six Activities with associated XML layout files:**

- MainActivity,     activity_main.xml
- DriveActivity,    activity_drive.xml
- OcrActivity,      activity_ocr.xml
- LogBookActivity,  activity_logbook.xml
- FilterActivity,   activity_filter.xml
- OptionsActivity,  activity_options.xml

**And two Java Classes (helper classes):**
- CustomAdapter
- MyDatabaseHelper


#### MainActivity:

Main menu of the App. Displays buttons to navigate to all different areas / activities of the application.

#### DriveActivity:

Here, users can start a new drive. After entering the start data and pressing the Drive button, the trip begins. The STOP button ends the trip. After entering the arrival data, the trip can be saved in the SQL database with the SAVE button. There are graphical UI elements for date and time that can be accessed via buttons next to the text field.
Users can manually enter the mileage or use the camera symbol to initiate text recognition to scan the mileage.
Trips are saved in a SQLite database using the MyDatabaseHelper helper class.

#### OcrActivity:

The TAKE PICTURE button initiates text recognition via the phone's camera. A photo can be taken and cropped to the desired area by the user. The scan appears in the mileage field and can be sent back to the DriveActivity via the OK button. Two libraries were imported for this:
- Recognize text in images with [ML Kit](https://developers.google.com/ml-kit/vision/text-recognition/v2/android)
- Select the area in the image to scan with [Android-Image-Cropper](https://github.com/ArthurHub/Android-Image-Cropper)


#### LogBookActivity:

This activity retrieves all saved trips from the SQL database and displays them in a tabular format.
The activity fetches data from the SQLite database using the MyDatabaseHelper helper class, stores it in ArrayLists, and displays it in a RecyclerView using the CustomAdapter helper class.
A RecyclerView is a UI component provided by the Android framework for displaying sets of data in a list or grid format.

#### FilterActivity:

Similar in structure and function to the LogBookActivity but modified to filter by name through a text field.

#### OptionsActivity:

Currently, only switching between English and German languages is possible here. It's worth noting that all texts appearing in the app are not hardcoded strings but exist as IDs referring to entries in strings.xml files. Separate strings.xml files exist for different languages. Thus, by selecting the desired strings.xml, all words can be displayed in the desired language.

#### CustomAdapter:

This adapter is designed to work with a RecyclerView to display the trips' data in a list format. The CustomAdapter class serves as a bridge between the trips' data and the RecyclerView.

#### MyDatabaseHelper:

This class serves as a helper class to interact with the SQLite database, providing methods to manage the database. Inside here are all the string queries for SQLite that are needed to manipulate the database.
