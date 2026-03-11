CP DIRECTLY FROM HERE OR REMOVE "&nbsp;" from notepad then cp


1\. Create an android application to pass the data from one activity to another activity

in the same application using intent (P3)

-->

1\. Modifying MainActivity.kt



Edit the MainActivity.kt file as follows

package com.example.quest1



import android.content.Intent

import android.os.Bundle

import androidx.activity.ComponentActivity

import androidx.activity.compose.setContent

import androidx.compose.foundation.layout.\*

import androidx.compose.material3.\*

import androidx.compose.runtime.\*

import androidx.compose.ui.Modifier

import androidx.compose.ui.unit.dp

import androidx.compose.ui.platform.LocalContext



class MainActivity : ComponentActivity() {

   override fun onCreate(savedInstanceState: Bundle?) {

       super.onCreate(savedInstanceState)

       setContent {

          MainScreen()

       }

   }

}



@OptIn(ExperimentalMaterial3Api::class)

@Composable

fun MainScreen() {

   val context = LocalContext.current

   var name by remember { mutableStateOf("") }



   Column(

       modifier = Modifier

           .fillMaxSize()

           .padding(16.dp)

   ){

       Text(

           text = "Main Activity",

           style = MaterialTheme.typography.headlineLarge

       )

       Spacer(modifier = Modifier.height(20.dp))



       OutlinedTextField(

           value = name,

           onValueChange = {name = it},

           label = {Text("Enter Your Name: ")}

       )



       Spacer(modifier = Modifier.height(20.dp))



       Button(onClick = {

           val intent = Intent(context, SecondActivity::class.java)

           intent.putExtra("username", name)

           context.startActivity(intent)

       }){

           Text("Send Data")

       }

   }

}



2\. Creating SecondActivity.kt (Steps)



Right click java → com.example.activitydemo



Click New → Kotlin Class/File



Name the file SecondActivity



Select Class and click OK



3\. Modifying SecondActivity.kt



Edit the SecondActivity.kt file as follows:



package com.example.quest1



import android.os.Bundle

import androidx.activity.ComponentActivity

import androidx.activity.compose.setContent

import androidx.compose.foundation.layout.\*

import androidx.compose.material3.\*

import androidx.compose.runtime.Composable

import androidx.compose.ui.Modifier

import androidx.compose.ui.unit.dp



class SecondActivity : ComponentActivity() {



   override fun onCreate(savedInstanceState: Bundle?) {

       super.onCreate(savedInstanceState)



       val receivedName = intent.getStringExtra("username")



       setContent {

           SecondScreen(receivedName ?: "")

       }

   }

}



@Composable

fun SecondScreen(name: String){



   Column(

       modifier = Modifier

           .fillMaxSize()

           .padding(16.dp)

   ){



       Text(

           text = "Second Activity",

           style = MaterialTheme.typography.headlineLarge

       )



       Spacer(modifier = Modifier.height(20.dp))



       Text(

           text = "Received Data: $name",

           style = MaterialTheme.typography.bodyLarge

       )

   }

}





4\. Modifying AndroidManifest.xml



Add SecondActivity inside the <application> tag.



<activity android:name=".SecondActivity"/>



5\. Configuring build.gradle.kts (Module:app)



plugins {

   id("com.android.application")

   id("org.jetbrains.kotlin.android")

}



android {

   namespace = "com.example.quest1"

   compileSdk = 35



   defaultConfig {

       applicationId = "com.example.quest1"

       minSdk = 24

       targetSdk = 35

       versionCode = 1

       versionName = "1.0"



       testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"

       vectorDrawables {

           useSupportLibrary = true

       }

   }



   buildTypes {

       release {

           isMinifyEnabled = false

           proguardFiles(

               getDefaultProguardFile("proguard-android-optimize.txt"),

               "proguard-rules.pro"

           )

       }

   }

   compileOptions {

       sourceCompatibility = JavaVersion.VERSION\_1\_8

       targetCompatibility = JavaVersion.VERSION\_1\_8

   }

   kotlinOptions {

       jvmTarget = "1.8"

   }

   buildFeatures {

       compose = true

   }

   composeOptions {

       kotlinCompilerExtensionVersion = "1.4.3"

   }

   packaging {

       resources {

           excludes += "/META-INF/{AL2.0,LGPL2.1}"

       }

   }

}



dependencies {



   implementation("androidx.core:core-ktx:1.9.0")

   implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

   implementation("androidx.activity:activity-compose:1.10.0")

   implementation(platform("androidx.compose:compose-bom:2023.03.00"))

   implementation("androidx.compose.ui:ui")

   implementation("androidx.compose.ui:ui-graphics")

   implementation("androidx.compose.ui:ui-tooling-preview")

   implementation("androidx.compose.material3:material3")

   implementation("androidx.appcompat:appcompat:1.6.1")

   implementation("com.google.android.material:material:1.8.0")

   implementation("androidx.constraintlayout:constraintlayout:2.1.4")

   testImplementation("junit:junit:4.13.2")

   androidTestImplementation("androidx.test.ext:junit:1.3.0")

   androidTestImplementation("androidx.test.espresso:espresso-core:3.7.0")

   androidTestImplementation(platform("androidx.compose:compose-bom:2023.03.00"))

   androidTestImplementation("androidx.compose.ui:ui-test-junit4")

   debugImplementation("androidx.compose.ui:ui-tooling")

   debugImplementation("androidx.compose.ui:ui-test-manifest")

}



7\. Configuring gradle-wrapper.properties

distributionBase=GRADLE\_USER\_HOME

distributionPath=wrapper/dists

distributionUrl=https\\://services.gradle.org/distributions/gradle-8.5-bin.zip

zipStoreBase=GRADLE\_USER\_HOME

zipStorePath=wrapper/dists

--------------------------------------------------------------



2\. Create a user interface with a TextView, Button, and ImageView. When the button is clicked, the image should be changed dynamically

-->

1\. Modifying MainActivity.kt

package com.example.quest2



import android.os.Bundle

import androidx.activity.ComponentActivity

import androidx.activity.compose.setContent

import androidx.compose.foundation.Image

import androidx.compose.foundation.layout.\*

import androidx.compose.material3.\*

import androidx.compose.runtime.\*

import androidx.compose.ui.Modifier

import androidx.compose.ui.res.painterResource

import androidx.compose.ui.unit.dp

import androidx.compose.ui.Alignment



class MainActivity : ComponentActivity() {

   override fun onCreate(savedInstanceState: Bundle?) {

       super.onCreate(savedInstanceState)

       setContent {

           MainScreen()

       }

   }

}



@Composable

fun MainScreen() {



   var imageChanged by remember { mutableStateOf(false) }



   Column(

       modifier = Modifier

           .fillMaxSize()

           .padding(16.dp),

       horizontalAlignment = Alignment.CenterHorizontally

   ){



       Text(

           text = "Dynamic Image Change",

           style = MaterialTheme.typography.headlineLarge

       )



       Spacer(modifier = Modifier.height(20.dp))



       Image(

           painter = painterResource(

               id = if(imageChanged) R.drawable.wp2 else R.drawable.wp

           ),

           contentDescription = "Dynamic Image",

           modifier = Modifier.size(200.dp)

       )



       Spacer(modifier = Modifier.height(20.dp))



       Button(onClick = {

           imageChanged = !imageChanged

       }){

           Text("Change Image")

       }

   }

}



2\. Adding Images to Drawable (Steps)



Open res → drawable folder.



Add two images.



Example:

image1.png

image2.png



These images will be used to dynamically change the ImageView when the button is clicked.



3\. Configuring build.gradle.kts (Module:app)



Modify build.gradle.kts (Module: app) as follows:



plugins {

   id("com.android.application")

   id("org.jetbrains.kotlin.android")

}



android {

   namespace = "com.example.quest2"

   compileSdk = 35



   defaultConfig {

       applicationId = "com.example.quest2"

       minSdk = 24

       targetSdk = 35

       versionCode = 1

       versionName = "1.0"



       testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"

       vectorDrawables {

           useSupportLibrary = true

       }

   }



   buildTypes {

       release {

           isMinifyEnabled = false

           proguardFiles(

               getDefaultProguardFile("proguard-android-optimize.txt"),

               "proguard-rules.pro"

           )

       }

   }

   compileOptions {

       sourceCompatibility = JavaVersion.VERSION\_1\_8

       targetCompatibility = JavaVersion.VERSION\_1\_8

   }

   kotlinOptions {

       jvmTarget = "1.8"

   }

   buildFeatures {

       compose = true

   }

   composeOptions {

       kotlinCompilerExtensionVersion = "1.4.3"

   }

   packaging {

       resources {

           excludes += "/META-INF/{AL2.0,LGPL2.1}"

       }

   }

}



dependencies {



   implementation("androidx.core:core-ktx:1.9.0")

   implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

   implementation("androidx.activity:activity-compose:1.10.0")

   implementation(platform("androidx.compose:compose-bom:2023.03.00"))

   implementation("androidx.compose.ui:ui")

   implementation("androidx.compose.ui:ui-graphics")

   implementation("androidx.compose.ui:ui-tooling-preview")

   implementation("androidx.compose.material3:material3")

   implementation("androidx.appcompat:appcompat:1.6.1")

   testImplementation("junit:junit:4.13.2")

   androidTestImplementation("androidx.test.ext:junit:1.3.0")

   androidTestImplementation("androidx.test.espresso:espresso-core:3.7.0")

   androidTestImplementation(platform("androidx.compose:compose-bom:2023.03.00"))

   androidTestImplementation("androidx.compose.ui:ui-test-junit4")

   debugImplementation("androidx.compose.ui:ui-tooling")

   debugImplementation("androidx.compose.ui:ui-test-manifest")

}



4\. Configuring gradle-wrapper.properties



Set the gradle-wrapper.properties correctly:



distributionBase=GRADLE\_USER\_HOME

distributionPath=wrapper/dists

distributionUrl=https\\://services.gradle.org/distributions/gradle-8.5-bin.zip

zipStoreBase=GRADLE\_USER\_HOME

zipStorePath=wrapper/dists

---



3\. Implement a custom color scheme for your registration form. Set the background color of the entire layout to a light color, and use a contrasting color for the Submit button.

-->

1\. Modifying MainActivity.kt



Edit the MainActivity.kt file as follows:

package com.example.activitydemo



package com.example.quest3



import android.os.Bundle

import androidx.activity.ComponentActivity

import androidx.activity.compose.setContent

import androidx.compose.foundation.background

import androidx.compose.foundation.layout.\*

import androidx.compose.material3.\*

import androidx.compose.runtime.Composable

import androidx.compose.ui.\*

import androidx.compose.ui.graphics.Color

import androidx.compose.ui.unit.dp



class MainActivity : ComponentActivity() {

   override fun onCreate(savedInstanceState: Bundle?) {

       super.onCreate(savedInstanceState)

       setContent {

           RegistrationForm()

       }

   }

}



@OptIn(ExperimentalMaterial3Api::class)

@Composable

fun RegistrationForm() {

   Column(

       modifier = Modifier

           .fillMaxSize()

           .background(Color.Yellow)

           .padding(16.dp),

       horizontalAlignment = Alignment.CenterHorizontally

   ){

       Text(

           text = "Registration Form",

           style = MaterialTheme.typography.headlineLarge

       )



       Spacer(modifier = Modifier.height(20.dp))



       OutlinedTextField(

           value = "",

           onValueChange = {},

           label = {Text("Enter Name")}

       )



       Spacer(modifier = Modifier.height(10.dp))



       OutlinedTextField(

           value = "",

           onValueChange = {},

           label = {Text("Enter Email")}

       )



       Spacer(modifier = Modifier.height(20.dp))





       Button(

           onClick = {},

           colors = ButtonDefaults.buttonColors(

               containerColor = Color.Magenta

           )

       ){

           Text("Submit", color = Color.White)

       }

   }

}





2\. Configuring build.gradle.kts (Module:app)



Modify build.gradle.kts (Module: app) as follows:

plugins {

   id("com.android.application")

   id("org.jetbrains.kotlin.android")

}



android {

   namespace = "com.example.quest3"

   compileSdk = 35



   defaultConfig {

       applicationId = "com.example.quest3"

       minSdk = 24

       targetSdk = 35

       versionCode = 1

       versionName = "1.0"



       testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"

       vectorDrawables {

           useSupportLibrary = true

       }

   }



   buildTypes {

       release {

           isMinifyEnabled = false

           proguardFiles(

               getDefaultProguardFile("proguard-android-optimize.txt"),

               "proguard-rules.pro"

           )

       }

   }

   compileOptions {

       sourceCompatibility = JavaVersion.VERSION\_1\_8

       targetCompatibility = JavaVersion.VERSION\_1\_8

   }

   kotlinOptions {

       jvmTarget = "1.8"

   }

   buildFeatures {

       compose = true

   }

   composeOptions {

       kotlinCompilerExtensionVersion = "1.4.3"

   }

   packaging {

       resources {

           excludes += "/META-INF/{AL2.0,LGPL2.1}"

       }

   }

}



dependencies {



   implementation("androidx.core:core-ktx:1.9.0")

   implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

   implementation("androidx.activity:activity-compose:1.10.0")

   implementation(platform("androidx.compose:compose-bom:2023.03.00"))

   implementation("androidx.compose.ui:ui")

   implementation("androidx.compose.ui:ui-graphics")

   implementation("androidx.compose.ui:ui-tooling-preview")

   implementation("androidx.compose.material3:material3")

   testImplementation("junit:junit:4.13.2")

   androidTestImplementation("androidx.test.ext:junit:1.3.0")

   androidTestImplementation("androidx.test.espresso:espresso-core:3.7.0")

   androidTestImplementation(platform("androidx.compose:compose-bom:2023.03.00"))

   androidTestImplementation("androidx.compose.ui:ui-test-junit4")

   debugImplementation("androidx.compose.ui:ui-tooling")

   debugImplementation("androidx.compose.ui:ui-test-manifest")

}



3\. Configuring gradle-wrapper.properties



Set the gradle-wrapper.properties correctly:



distributionBase=GRADLE\_USER\_HOME

distributionPath=wrapper/dists

distributionUrl=https\\://services.gradle.org/distributions/gradle-8.5-bin.zip

zipStoreBase=GRADLE\_USER\_HOME

zipStorePath=wrapper/dists



---



4\. Insert the new contents in the following resources and demonstrate their uses in the android application

Android Resources: (Color, Theme, String, Drawable, Dimension, Image)(P2)



1\. Modifying MainActivity.kt



Edit the MainActivity.kt file as follows:

package com.example.activitydemo



package com.example.quest4



import android.os.Bundle

import androidx.activity.ComponentActivity

import androidx.activity.compose.setContent

import androidx.compose.foundation.Image

import androidx.compose.foundation.background

import androidx.compose.foundation.layout.\*

import androidx.compose.material3.\*

import androidx.compose.runtime.Composable

import androidx.compose.ui.\*

import androidx.compose.ui.unit.dp

import androidx.compose.ui.res.\*

import androidx.compose.ui.graphics.Color



class MainActivity : ComponentActivity() {

   override fun onCreate(savedInstanceState: Bundle?) {

       super.onCreate(savedInstanceState)

       setContent {

           ResourceDemo()

       }

   }

}



@Composable

fun ResourceDemo() {

   Column(

       modifier = Modifier

           .fillMaxSize()

           .background(colorResource(id = R.color.backgroundColor))

           .padding(dimensionResource(id = R.dimen.padding\_large)),

       horizontalAlignment = Alignment.CenterHorizontally

   ){

       Text(

           text = stringResource(id = R.string.app\_title),

           style = MaterialTheme.typography.headlineLarge,

           color = colorResource(id = R.color.textColor)

       )



       Spacer(modifier = Modifier.height(20.dp))



       Image(

           painter = painterResource(id = R.drawable.cat),

           contentDescription = "cat",

           modifier = Modifier.size(200.dp)

       )



       Spacer(modifier = Modifier.height(20.dp))

       }

   }



2\. Modifying strings.xml



Insert the following contents in res/values/strings.xml:



<resources>

   <string name="app\_name">ResourceDemoApp</string>

   <string name="app\_title">Android Resource Demo</string>

</resources>



3\. Modifying colors.xml



Insert the following contents in res/values/colors.xml:



<?xml version="1.0" encoding="utf-8"?>

<resources>



   <color name="backgroundColor">#FFF3E0</color>

   <color name="textColor">#000000</color>



</resources>



4\. Modifying dimens.xml



Create res/values/dimens.xml and insert:



<?xml version="1.0" encoding="utf-8"?>

<resources>

   <dimen name="padding\_large">24dp</dimen>

</resources>



5\. Adding Drawable Resource



Add an image in res/drawable folder.



Example:



sample\_image.**png**



This image will be used in the Image component.



6\. Modifying themes.xml



Insert or modify res/values/themes.xml:



<?xml version="1.0" encoding="utf-8"?>

<resources>



   <style name="Theme.Quest4" parent="Theme.MaterialComponents.DayNight.NoActionBar">

       <item name="colorPrimary">@color/textColor</item>

   </style>



</resources>



7\. Configuring build.gradle.kts (Module:app)



plugins {

   id("com.android.application")

   id("org.jetbrains.kotlin.android")

}



android {

   namespace = "com.example.quest4"

   compileSdk = 35



   defaultConfig {

       applicationId = "com.example.quest4"

       minSdk = 24

       targetSdk = 35

       versionCode = 1

       versionName = "1.0"



       testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"

       vectorDrawables {

           useSupportLibrary = true

       }

   }



   buildTypes {

       release {

           isMinifyEnabled = false

           proguardFiles(

               getDefaultProguardFile("proguard-android-optimize.txt"),

               "proguard-rules.pro"

           )

       }

   }

   compileOptions {

       sourceCompatibility = JavaVersion.VERSION\_1\_8

       targetCompatibility = JavaVersion.VERSION\_1\_8

   }

   kotlinOptions {

       jvmTarget = "1.8"

   }

   buildFeatures {

       compose = true

   }

   composeOptions {

       kotlinCompilerExtensionVersion = "1.4.3"

   }

   packaging {

       resources {

           excludes += "/META-INF/{AL2.0,LGPL2.1}"

       }

   }

}



dependencies {



   implementation("androidx.core:core-ktx:1.9.0")

   implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

   implementation("androidx.activity:activity-compose:1.10.0")

   implementation(platform("androidx.compose:compose-bom:2023.03.00"))



   implementation("androidx.compose.ui:ui")

   implementation("androidx.compose.ui:ui-graphics")

   implementation("androidx.compose.ui:ui-tooling-preview")



   implementation("androidx.compose.material3:material3")

   implementation("androidx.constraintlayout:constraintlayout:2.1.4")

   implementation("com.google.android.material:material:1.11.0")

   testImplementation("junit:junit:4.13.2")

   androidTestImplementation("androidx.test.ext:junit:1.1.5")

   androidTestImplementation("androidx.test.espresso:espresso-core:3.5.1")

   androidTestImplementation(platform("androidx.compose:compose-bom:2023.03.00"))

   androidTestImplementation("androidx.compose.ui:ui-test-junit4")

   debugImplementation("androidx.compose.ui:ui-tooling")

   debugImplementation("androidx.compose.ui:ui-test-manifest")



}



8\. Configuring gradle-wrapper.properties



distributionBase=GRADLE\_USER\_HOME

distributionPath=wrapper/dists

distributionUrl=https\\://services.gradle.org/distributions/gradle-8.5-bin.zip

zipStoreBase=GRADLE\_USER\_HOME

zipStorePath=wrapper/dists

---



5\. Create an android application and  print “hello world” program(P1)

-->

1\. Modifying MainActivity.kt



Edit the MainActivity.kt file as follows:

package com.example.myapplication



import android.os.Bundle

import androidx.activity.ComponentActivity

import androidx.activity.compose.setContent

import androidx.compose.foundation.layout.\*

import androidx.compose.material3.\*

import androidx.compose.runtime.Composable

import androidx.compose.ui.Alignment

import androidx.compose.ui.Modifier

import androidx.compose.ui.unit.dp

import androidx.compose.ui.tooling.preview.Preview

import com.example.myapplication.ui.theme.MyApplicationTheme





class MainActivity : ComponentActivity() {

   override fun onCreate(savedInstanceState: Bundle?) {

       super.onCreate(savedInstanceState)

       setContent {

           HelloWorldScreen()

       }

   }

}

@Composable

fun HelloWorldScreen() {

   Column(

       modifier = Modifier

           .fillMaxSize()

           .padding(16.dp),

       horizontalAlignment = Alignment.CenterHorizontally,

       verticalArrangement = Arrangement.Center

   ){

       Text(

           text = "Hello World",

            style = MaterialTheme.typography.headlineLarge

       )

   }

}





2\. Configuring build.gradle.kts (Module:app)



Modify build.gradle.kts (Module: app) as follows:

plugins {

   id("com.android.application")

   id("org.jetbrains.kotlin.android")

}



android {

   namespace = "com.example.myapplication"

   compileSdk = 35



   defaultConfig {

       applicationId = "com.example.myapplication"

       minSdk = 24

       targetSdk = 35

       versionCode = 1

       versionName = "1.0"



       testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"

       vectorDrawables {

           useSupportLibrary = true

       }

   }



   buildTypes {

       release {

           isMinifyEnabled = false

           proguardFiles(

               getDefaultProguardFile("proguard-android-optimize.txt"),

               "proguard-rules.pro"

           )

       }

   }

   compileOptions {

       sourceCompatibility = JavaVersion.VERSION\_1\_8

       targetCompatibility = JavaVersion.VERSION\_1\_8

   }

   kotlinOptions {

       jvmTarget = "1.8"

   }

   buildFeatures {

       compose = true

   }

   composeOptions {

       kotlinCompilerExtensionVersion = "1.4.3"

   }

   packaging {

       resources {

           excludes += "/META-INF/{AL2.0,LGPL2.1}"

       }

   }

}



dependencies {



   implementation("androidx.core:core-ktx:1.9.0")

   implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.10.0")

   implementation("androidx.activity:activity-compose:1.10.0")

   implementation(platform("androidx.compose:compose-bom:2023.03.00"))

   implementation("androidx.compose.ui:ui")

   implementation("androidx.compose.ui:ui-graphics")

   implementation("androidx.compose.ui:ui-tooling-preview")

   implementation("androidx.compose.material3:material3")

   implementation("androidx.appcompat:appcompat:1.6.1")

   testImplementation("junit:junit:4.13.2")

   androidTestImplementation("androidx.test.ext:junit:1.3.0")

   androidTestImplementation("androidx.test.espresso:espresso-core:3.7.0")

   androidTestImplementation(platform("androidx.compose:compose-bom:2023.03.00"))

   androidTestImplementation("androidx.compose.ui:ui-test-junit4")

   debugImplementation("androidx.compose.ui:ui-tooling")

   debugImplementation("androidx.compose.ui:ui-test-manifest")

}



3\. Configuring gradle-wrapper.properties



Set the gradle-wrapper.properties correctly:



distributionBase=GRADLE\_USER\_HOME

distributionPath=wrapper/dists

distributionUrl=https\\://services.gradle.org/distributions/gradle-8.5-bin.zip

zipStoreBase=GRADLE\_USER\_HOME

zipStorePath=wrapper/dists

---



6\. Create a simple Registration Form with the following fields:

•	Name (Text Input)

•	Email (Text Input)

•	Phone Number (Text Input)

•	Password (Password Input)

•	Confirm Password (Password Input)

•	Submit Button

-->

1\. Modifying MainActivity.kt



Edit the MainActivity.kt file as follows:

package com.example.activitydemo



import android.os.Bundle

import androidx.activity.ComponentActivity

import androidx.activity.compose.setContent

import androidx.compose.foundation.layout.\*

import androidx.compose.material3.\*

import androidx.compose.runtime.\*

import androidx.compose.ui.Modifier

import androidx.compose.ui.text.input.PasswordVisualTransformation

import androidx.compose.ui.unit.dp

import androidx.compose.ui.Alignment



class MainActivity : ComponentActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {

        super.onCreate(savedInstanceState)



        setContent {

            RegistrationForm()

        }

    }

}



@Composable

fun RegistrationForm(){



    var name by remember { mutableStateOf("") }

    var email by remember { mutableStateOf("") }

    var phone by remember { mutableStateOf("") }

    var password by remember { mutableStateOf("") }

    var confirmPassword by remember { mutableStateOf("") }



    Column(

        modifier = Modifier

            .fillMaxSize()

            .padding(16.dp),

        horizontalAlignment = Alignment.CenterHorizontally

    ){



        Text(

            text = "Registration Form",

            style = MaterialTheme.typography.headlineLarge

        )



        Spacer(modifier = Modifier.height(20.dp))



        OutlinedTextField(

            value = name,

            onValueChange = { name = it },

            label = { Text("Name") }

        )



        Spacer(modifier = Modifier.height(10.dp))



        OutlinedTextField(

            value = email,

            onValueChange = { email = it },

            label = { Text("Email") }

        )



        Spacer(modifier = Modifier.height(10.dp))



        OutlinedTextField(

            value = phone,

            onValueChange = { phone = it },

            label = { Text("Phone Number") }

        )



        Spacer(modifier = Modifier.height(10.dp))



        OutlinedTextField(

            value = password,

            onValueChange = { password = it },

            label = { Text("Password") },

            visualTransformation = PasswordVisualTransformation()

        )



        Spacer(modifier = Modifier.height(10.dp))



        OutlinedTextField(

            value = confirmPassword,

            onValueChange = { confirmPassword = it },

            label = { Text("Confirm Password") },

            visualTransformation = PasswordVisualTransformation()

        )



        Spacer(modifier = Modifier.height(20.dp))



        Button(onClick = { }) {

            Text("Submit")

        }

    }

}



2\. Configuring build.gradle.kts (Module:app)



Modify build.gradle.kts (Module: app) as follows:



plugins {

    id("com.android.application")

    id("org.jetbrains.kotlin.android")

}



android {

    namespace = "com.example.activitydemo"

    compileSdk = 35



    defaultConfig {

        applicationId = "com.example.activitydemo"

        minSdk = 24

        targetSdk = 35

        versionCode = 1

        versionName = "1.0"



        testInstrumentationRunner =

            "androidx.test.runner.AndroidJUnitRunner"

    }



    buildFeatures {

        compose = true

    }



    composeOptions {

        kotlinCompilerExtensionVersion = "1.4.3"

    }



    compileOptions {

        sourceCompatibility = JavaVersion.VERSION\_1\_8

        targetCompatibility = JavaVersion.VERSION\_1\_8

    }



    kotlinOptions {

        jvmTarget = "1.8"

    }

}



dependencies {



    implementation("androidx.core:core-ktx:1.9.0")

    implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

    implementation("androidx.activity:activity-compose:1.10.0")



    implementation(platform("androidx.compose:compose-bom:2023.03.00"))

    implementation("androidx.compose.ui:ui")

    implementation("androidx.compose.ui:ui-graphics")

    implementation("androidx.compose.ui:ui-tooling-preview")

    implementation("androidx.compose.material3:material3")



    implementation("androidx.appcompat:appcompat:1.6.1")

    implementation("com.google.android.material:material:1.8.0")

}



3\. Configuring gradle-wrapper.properties



Set the gradle-wrapper.properties correctly:



distributionBase=GRADLE\_USER\_HOME

distributionPath=wrapper/dists

distributionUrl=https\\://services.gradle.org/distributions/gradle-8.5-bin.zip

zipStoreBase=GRADLE\_USER\_HOME

zipStorePath=wrapper/dists



---



7\. Create a Registration Form with the following fields:

•	Username (Text Input)

•	Email Address (Text Input)

•	Gender (Radio Buttons with options "Male" and "Female")

•	Password (Password Input)

•	Submit Button

-->

1\. Modifying MainActivity.kt



Edit the MainActivity.kt file as follows:

package com.example.activitydemo



import android.os.Bundle

import androidx.activity.ComponentActivity

import androidx.activity.compose.setContent

import androidx.compose.foundation.layout.\*

import androidx.compose.material3.\*

import androidx.compose.runtime.\*

import androidx.compose.ui.Modifier

import androidx.compose.ui.text.input.PasswordVisualTransformation

import androidx.compose.ui.unit.dp

import androidx.compose.ui.Alignment



class MainActivity : ComponentActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {

        super.onCreate(savedInstanceState)



        setContent {

            RegistrationForm()

        }

    }

}



@Composable

fun RegistrationForm(){



    var username by remember { mutableStateOf("") }

    var email by remember { mutableStateOf("") }

    var password by remember { mutableStateOf("") }

    var gender by remember { mutableStateOf("Male") }



    Column(

        modifier = Modifier

            .fillMaxSize()

            .padding(16.dp)

    ){



        Text(

            text = "Registration Form",

            style = MaterialTheme.typography.headlineLarge

        )



        Spacer(modifier = Modifier.height(20.dp))



        OutlinedTextField(

            value = username,

            onValueChange = { username = it },

            label = { Text("Username") }

        )



        Spacer(modifier = Modifier.height(10.dp))



        OutlinedTextField(

            value = email,

            onValueChange = { email = it },

            label = { Text("Email Address") }

        )



        Spacer(modifier = Modifier.height(20.dp))



        Text("Select Gender")



        Row(

            verticalAlignment = Alignment.CenterVertically

        ){



            RadioButton(

                selected = gender == "Male",

                onClick = { gender = "Male" }

            )

            Text("Male")



            Spacer(modifier = Modifier.width(20.dp))



            RadioButton(

                selected = gender == "Female",

                onClick = { gender = "Female" }

            )

            Text("Female")

        }



        Spacer(modifier = Modifier.height(20.dp))



        OutlinedTextField(

            value = password,

            onValueChange = { password = it },

            label = { Text("Password") },

            visualTransformation = PasswordVisualTransformation()

        )



        Spacer(modifier = Modifier.height(20.dp))



        Button(onClick = { }) {

            Text("Submit")

        }

    }

}



2\. Configuring build.gradle.kts (Module:app)



Modify build.gradle.kts (Module: app) as follows:

plugins {

    id("com.android.application")

    id("org.jetbrains.kotlin.android")

}



android {

    namespace = "com.example.activitydemo"

    compileSdk = 35



    defaultConfig {

        applicationId = "com.example.activitydemo"

        minSdk = 24

        targetSdk = 35

        versionCode = 1

        versionName = "1.0"



        testInstrumentationRunner =

            "androidx.test.runner.AndroidJUnitRunner"

    }



    buildFeatures {

        compose = true

    }



    composeOptions {

        kotlinCompilerExtensionVersion = "1.4.3"

    }



    compileOptions {

        sourceCompatibility = JavaVersion.VERSION\_1\_8

        targetCompatibility = JavaVersion.VERSION\_1\_8

    }



    kotlinOptions {

        jvmTarget = "1.8"

    }

}



dependencies {



    implementation("androidx.core:core-ktx:1.9.0")

    implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

    implementation("androidx.activity:activity-compose:1.10.0")



    implementation(platform("androidx.compose:compose-bom:2023.03.00"))

    implementation("androidx.compose.ui:ui")

    implementation("androidx.compose.ui:ui-graphics")

    implementation("androidx.compose.ui:ui-tooling-preview")

    implementation("androidx.compose.material3:material3")



    implementation("androidx.appcompat:appcompat:1.6.1")

    implementation("com.google.android.material:material:1.8.0")

}



3\. Configuring gradle-wrapper.properties



Set the gradle-wrapper.properties correctly:



distributionBase=GRADLE\_USER\_HOME

distributionPath=wrapper/dists

distributionUrl=https\\://services.gradle.org/distributions/gradle-8.5-bin.zip

zipStoreBase=GRADLE\_USER\_HOME

zipStorePath=wrapper/dists


