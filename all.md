practice questions for AP practical



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

&nbsp;   override fun onCreate(savedInstanceState: Bundle?) {

&nbsp;       super.onCreate(savedInstanceState)

&nbsp;       setContent {

&nbsp;          MainScreen()

&nbsp;       }

&nbsp;   }

}



@OptIn(ExperimentalMaterial3Api::class)

@Composable

fun MainScreen() {

&nbsp;   val context = LocalContext.current

&nbsp;   var name by remember { mutableStateOf("") }



&nbsp;   Column(

&nbsp;       modifier = Modifier

&nbsp;           .fillMaxSize()

&nbsp;           .padding(16.dp)

&nbsp;   ){

&nbsp;       Text(

&nbsp;           text = "Main Activity",

&nbsp;           style = MaterialTheme.typography.headlineLarge

&nbsp;       )

&nbsp;       Spacer(modifier = Modifier.height(20.dp))



&nbsp;       OutlinedTextField(

&nbsp;           value = name,

&nbsp;           onValueChange = {name = it},

&nbsp;           label = {Text("Enter Your Name: ")}

&nbsp;       )



&nbsp;       Spacer(modifier = Modifier.height(20.dp))



&nbsp;       Button(onClick = {

&nbsp;           val intent = Intent(context, SecondActivity::class.java)

&nbsp;           intent.putExtra("username", name)

&nbsp;           context.startActivity(intent)

&nbsp;       }){

&nbsp;           Text("Send Data")

&nbsp;       }

&nbsp;   }

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



&nbsp;   override fun onCreate(savedInstanceState: Bundle?) {

&nbsp;       super.onCreate(savedInstanceState)



&nbsp;       val receivedName = intent.getStringExtra("username")



&nbsp;       setContent {

&nbsp;           SecondScreen(receivedName ?: "")

&nbsp;       }

&nbsp;   }

}



@Composable

fun SecondScreen(name: String){



&nbsp;   Column(

&nbsp;       modifier = Modifier

&nbsp;           .fillMaxSize()

&nbsp;           .padding(16.dp)

&nbsp;   ){



&nbsp;       Text(

&nbsp;           text = "Second Activity",

&nbsp;           style = MaterialTheme.typography.headlineLarge

&nbsp;       )



&nbsp;       Spacer(modifier = Modifier.height(20.dp))



&nbsp;       Text(

&nbsp;           text = "Received Data: $name",

&nbsp;           style = MaterialTheme.typography.bodyLarge

&nbsp;       )

&nbsp;   }

}





4\. Modifying AndroidManifest.xml



Add SecondActivity inside the <application> tag.



<activity android:name=".SecondActivity"/>



5\. Configuring build.gradle.kts (Module:app)



plugins {

&nbsp;   id("com.android.application")

&nbsp;   id("org.jetbrains.kotlin.android")

}



android {

&nbsp;   namespace = "com.example.quest1"

&nbsp;   compileSdk = 35



&nbsp;   defaultConfig {

&nbsp;       applicationId = "com.example.quest1"

&nbsp;       minSdk = 24

&nbsp;       targetSdk = 35

&nbsp;       versionCode = 1

&nbsp;       versionName = "1.0"



&nbsp;       testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"

&nbsp;       vectorDrawables {

&nbsp;           useSupportLibrary = true

&nbsp;       }

&nbsp;   }



&nbsp;   buildTypes {

&nbsp;       release {

&nbsp;           isMinifyEnabled = false

&nbsp;           proguardFiles(

&nbsp;               getDefaultProguardFile("proguard-android-optimize.txt"),

&nbsp;               "proguard-rules.pro"

&nbsp;           )

&nbsp;       }

&nbsp;   }

&nbsp;   compileOptions {

&nbsp;       sourceCompatibility = JavaVersion.VERSION\_1\_8

&nbsp;       targetCompatibility = JavaVersion.VERSION\_1\_8

&nbsp;   }

&nbsp;   kotlinOptions {

&nbsp;       jvmTarget = "1.8"

&nbsp;   }

&nbsp;   buildFeatures {

&nbsp;       compose = true

&nbsp;   }

&nbsp;   composeOptions {

&nbsp;       kotlinCompilerExtensionVersion = "1.4.3"

&nbsp;   }

&nbsp;   packaging {

&nbsp;       resources {

&nbsp;           excludes += "/META-INF/{AL2.0,LGPL2.1}"

&nbsp;       }

&nbsp;   }

}



dependencies {



&nbsp;   implementation("androidx.core:core-ktx:1.9.0")

&nbsp;   implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

&nbsp;   implementation("androidx.activity:activity-compose:1.10.0")

&nbsp;   implementation(platform("androidx.compose:compose-bom:2023.03.00"))

&nbsp;   implementation("androidx.compose.ui:ui")

&nbsp;   implementation("androidx.compose.ui:ui-graphics")

&nbsp;   implementation("androidx.compose.ui:ui-tooling-preview")

&nbsp;   implementation("androidx.compose.material3:material3")

&nbsp;   implementation("androidx.appcompat:appcompat:1.6.1")

&nbsp;   implementation("com.google.android.material:material:1.8.0")

&nbsp;   implementation("androidx.constraintlayout:constraintlayout:2.1.4")

&nbsp;   testImplementation("junit:junit:4.13.2")

&nbsp;   androidTestImplementation("androidx.test.ext:junit:1.3.0")

&nbsp;   androidTestImplementation("androidx.test.espresso:espresso-core:3.7.0")

&nbsp;   androidTestImplementation(platform("androidx.compose:compose-bom:2023.03.00"))

&nbsp;   androidTestImplementation("androidx.compose.ui:ui-test-junit4")

&nbsp;   debugImplementation("androidx.compose.ui:ui-tooling")

&nbsp;   debugImplementation("androidx.compose.ui:ui-test-manifest")

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

&nbsp;   override fun onCreate(savedInstanceState: Bundle?) {

&nbsp;       super.onCreate(savedInstanceState)

&nbsp;       setContent {

&nbsp;           MainScreen()

&nbsp;       }

&nbsp;   }

}



@Composable

fun MainScreen() {



&nbsp;   var imageChanged by remember { mutableStateOf(false) }



&nbsp;   Column(

&nbsp;       modifier = Modifier

&nbsp;           .fillMaxSize()

&nbsp;           .padding(16.dp),

&nbsp;       horizontalAlignment = Alignment.CenterHorizontally

&nbsp;   ){



&nbsp;       Text(

&nbsp;           text = "Dynamic Image Change",

&nbsp;           style = MaterialTheme.typography.headlineLarge

&nbsp;       )



&nbsp;       Spacer(modifier = Modifier.height(20.dp))



&nbsp;       Image(

&nbsp;           painter = painterResource(

&nbsp;               id = if(imageChanged) R.drawable.wp2 else R.drawable.wp

&nbsp;           ),

&nbsp;           contentDescription = "Dynamic Image",

&nbsp;           modifier = Modifier.size(200.dp)

&nbsp;       )



&nbsp;       Spacer(modifier = Modifier.height(20.dp))



&nbsp;       Button(onClick = {

&nbsp;           imageChanged = !imageChanged

&nbsp;       }){

&nbsp;           Text("Change Image")

&nbsp;       }

&nbsp;   }

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

&nbsp;   id("com.android.application")

&nbsp;   id("org.jetbrains.kotlin.android")

}



android {

&nbsp;   namespace = "com.example.quest2"

&nbsp;   compileSdk = 35



&nbsp;   defaultConfig {

&nbsp;       applicationId = "com.example.quest2"

&nbsp;       minSdk = 24

&nbsp;       targetSdk = 35

&nbsp;       versionCode = 1

&nbsp;       versionName = "1.0"



&nbsp;       testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"

&nbsp;       vectorDrawables {

&nbsp;           useSupportLibrary = true

&nbsp;       }

&nbsp;   }



&nbsp;   buildTypes {

&nbsp;       release {

&nbsp;           isMinifyEnabled = false

&nbsp;           proguardFiles(

&nbsp;               getDefaultProguardFile("proguard-android-optimize.txt"),

&nbsp;               "proguard-rules.pro"

&nbsp;           )

&nbsp;       }

&nbsp;   }

&nbsp;   compileOptions {

&nbsp;       sourceCompatibility = JavaVersion.VERSION\_1\_8

&nbsp;       targetCompatibility = JavaVersion.VERSION\_1\_8

&nbsp;   }

&nbsp;   kotlinOptions {

&nbsp;       jvmTarget = "1.8"

&nbsp;   }

&nbsp;   buildFeatures {

&nbsp;       compose = true

&nbsp;   }

&nbsp;   composeOptions {

&nbsp;       kotlinCompilerExtensionVersion = "1.4.3"

&nbsp;   }

&nbsp;   packaging {

&nbsp;       resources {

&nbsp;           excludes += "/META-INF/{AL2.0,LGPL2.1}"

&nbsp;       }

&nbsp;   }

}



dependencies {



&nbsp;   implementation("androidx.core:core-ktx:1.9.0")

&nbsp;   implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

&nbsp;   implementation("androidx.activity:activity-compose:1.10.0")

&nbsp;   implementation(platform("androidx.compose:compose-bom:2023.03.00"))

&nbsp;   implementation("androidx.compose.ui:ui")

&nbsp;   implementation("androidx.compose.ui:ui-graphics")

&nbsp;   implementation("androidx.compose.ui:ui-tooling-preview")

&nbsp;   implementation("androidx.compose.material3:material3")

&nbsp;   implementation("androidx.appcompat:appcompat:1.6.1")

&nbsp;   testImplementation("junit:junit:4.13.2")

&nbsp;   androidTestImplementation("androidx.test.ext:junit:1.3.0")

&nbsp;   androidTestImplementation("androidx.test.espresso:espresso-core:3.7.0")

&nbsp;   androidTestImplementation(platform("androidx.compose:compose-bom:2023.03.00"))

&nbsp;   androidTestImplementation("androidx.compose.ui:ui-test-junit4")

&nbsp;   debugImplementation("androidx.compose.ui:ui-tooling")

&nbsp;   debugImplementation("androidx.compose.ui:ui-test-manifest")

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

&nbsp;   override fun onCreate(savedInstanceState: Bundle?) {

&nbsp;       super.onCreate(savedInstanceState)

&nbsp;       setContent {

&nbsp;           RegistrationForm()

&nbsp;       }

&nbsp;   }

}



@OptIn(ExperimentalMaterial3Api::class)

@Composable

fun RegistrationForm() {

&nbsp;   Column(

&nbsp;       modifier = Modifier

&nbsp;           .fillMaxSize()

&nbsp;           .background(Color.Yellow)

&nbsp;           .padding(16.dp),

&nbsp;       horizontalAlignment = Alignment.CenterHorizontally

&nbsp;   ){

&nbsp;       Text(

&nbsp;           text = "Registration Form",

&nbsp;           style = MaterialTheme.typography.headlineLarge

&nbsp;       )



&nbsp;       Spacer(modifier = Modifier.height(20.dp))



&nbsp;       OutlinedTextField(

&nbsp;           value = "",

&nbsp;           onValueChange = {},

&nbsp;           label = {Text("Enter Name")}

&nbsp;       )



&nbsp;       Spacer(modifier = Modifier.height(10.dp))



&nbsp;       OutlinedTextField(

&nbsp;           value = "",

&nbsp;           onValueChange = {},

&nbsp;           label = {Text("Enter Email")}

&nbsp;       )



&nbsp;       Spacer(modifier = Modifier.height(20.dp))





&nbsp;       Button(

&nbsp;           onClick = {},

&nbsp;           colors = ButtonDefaults.buttonColors(

&nbsp;               containerColor = Color.Magenta

&nbsp;           )

&nbsp;       ){

&nbsp;           Text("Submit", color = Color.White)

&nbsp;       }

&nbsp;   }

}





2\. Configuring build.gradle.kts (Module:app)



Modify build.gradle.kts (Module: app) as follows:

plugins {

&nbsp;   id("com.android.application")

&nbsp;   id("org.jetbrains.kotlin.android")

}



android {

&nbsp;   namespace = "com.example.quest3"

&nbsp;   compileSdk = 35



&nbsp;   defaultConfig {

&nbsp;       applicationId = "com.example.quest3"

&nbsp;       minSdk = 24

&nbsp;       targetSdk = 35

&nbsp;       versionCode = 1

&nbsp;       versionName = "1.0"



&nbsp;       testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"

&nbsp;       vectorDrawables {

&nbsp;           useSupportLibrary = true

&nbsp;       }

&nbsp;   }



&nbsp;   buildTypes {

&nbsp;       release {

&nbsp;           isMinifyEnabled = false

&nbsp;           proguardFiles(

&nbsp;               getDefaultProguardFile("proguard-android-optimize.txt"),

&nbsp;               "proguard-rules.pro"

&nbsp;           )

&nbsp;       }

&nbsp;   }

&nbsp;   compileOptions {

&nbsp;       sourceCompatibility = JavaVersion.VERSION\_1\_8

&nbsp;       targetCompatibility = JavaVersion.VERSION\_1\_8

&nbsp;   }

&nbsp;   kotlinOptions {

&nbsp;       jvmTarget = "1.8"

&nbsp;   }

&nbsp;   buildFeatures {

&nbsp;       compose = true

&nbsp;   }

&nbsp;   composeOptions {

&nbsp;       kotlinCompilerExtensionVersion = "1.4.3"

&nbsp;   }

&nbsp;   packaging {

&nbsp;       resources {

&nbsp;           excludes += "/META-INF/{AL2.0,LGPL2.1}"

&nbsp;       }

&nbsp;   }

}



dependencies {



&nbsp;   implementation("androidx.core:core-ktx:1.9.0")

&nbsp;   implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

&nbsp;   implementation("androidx.activity:activity-compose:1.10.0")

&nbsp;   implementation(platform("androidx.compose:compose-bom:2023.03.00"))

&nbsp;   implementation("androidx.compose.ui:ui")

&nbsp;   implementation("androidx.compose.ui:ui-graphics")

&nbsp;   implementation("androidx.compose.ui:ui-tooling-preview")

&nbsp;   implementation("androidx.compose.material3:material3")

&nbsp;   testImplementation("junit:junit:4.13.2")

&nbsp;   androidTestImplementation("androidx.test.ext:junit:1.3.0")

&nbsp;   androidTestImplementation("androidx.test.espresso:espresso-core:3.7.0")

&nbsp;   androidTestImplementation(platform("androidx.compose:compose-bom:2023.03.00"))

&nbsp;   androidTestImplementation("androidx.compose.ui:ui-test-junit4")

&nbsp;   debugImplementation("androidx.compose.ui:ui-tooling")

&nbsp;   debugImplementation("androidx.compose.ui:ui-test-manifest")

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

&nbsp;   override fun onCreate(savedInstanceState: Bundle?) {

&nbsp;       super.onCreate(savedInstanceState)

&nbsp;       setContent {

&nbsp;           ResourceDemo()

&nbsp;       }

&nbsp;   }

}



@Composable

fun ResourceDemo() {

&nbsp;   Column(

&nbsp;       modifier = Modifier

&nbsp;           .fillMaxSize()

&nbsp;           .background(colorResource(id = R.color.backgroundColor))

&nbsp;           .padding(dimensionResource(id = R.dimen.padding\_large)),

&nbsp;       horizontalAlignment = Alignment.CenterHorizontally

&nbsp;   ){

&nbsp;       Text(

&nbsp;           text = stringResource(id = R.string.app\_title),

&nbsp;           style = MaterialTheme.typography.headlineLarge,

&nbsp;           color = colorResource(id = R.color.textColor)

&nbsp;       )



&nbsp;       Spacer(modifier = Modifier.height(20.dp))



&nbsp;       Image(

&nbsp;           painter = painterResource(id = R.drawable.cat),

&nbsp;           contentDescription = "cat",

&nbsp;           modifier = Modifier.size(200.dp)

&nbsp;       )



&nbsp;       Spacer(modifier = Modifier.height(20.dp))

&nbsp;       }

&nbsp;   }



2\. Modifying strings.xml



Insert the following contents in res/values/strings.xml:



<resources>

&nbsp;   <string name="app\_name">ResourceDemoApp</string>

&nbsp;   <string name="app\_title">Android Resource Demo</string>

</resources>



3\. Modifying colors.xml



Insert the following contents in res/values/colors.xml:



<?xml version="1.0" encoding="utf-8"?>

<resources>



&nbsp;   <color name="backgroundColor">#FFF3E0</color>

&nbsp;   <color name="textColor">#000000</color>



</resources>



4\. Modifying dimens.xml



Create res/values/dimens.xml and insert:



<?xml version="1.0" encoding="utf-8"?>

<resources>

&nbsp;   <dimen name="padding\_large">24dp</dimen>

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



&nbsp;   <style name="Theme.Quest4" parent="Theme.MaterialComponents.DayNight.NoActionBar">

&nbsp;       <item name="colorPrimary">@color/textColor</item>

&nbsp;   </style>



</resources>



7\. Configuring build.gradle.kts (Module:app)



plugins {

&nbsp;   id("com.android.application")

&nbsp;   id("org.jetbrains.kotlin.android")

}



android {

&nbsp;   namespace = "com.example.quest4"

&nbsp;   compileSdk = 35



&nbsp;   defaultConfig {

&nbsp;       applicationId = "com.example.quest4"

&nbsp;       minSdk = 24

&nbsp;       targetSdk = 35

&nbsp;       versionCode = 1

&nbsp;       versionName = "1.0"



&nbsp;       testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"

&nbsp;       vectorDrawables {

&nbsp;           useSupportLibrary = true

&nbsp;       }

&nbsp;   }



&nbsp;   buildTypes {

&nbsp;       release {

&nbsp;           isMinifyEnabled = false

&nbsp;           proguardFiles(

&nbsp;               getDefaultProguardFile("proguard-android-optimize.txt"),

&nbsp;               "proguard-rules.pro"

&nbsp;           )

&nbsp;       }

&nbsp;   }

&nbsp;   compileOptions {

&nbsp;       sourceCompatibility = JavaVersion.VERSION\_1\_8

&nbsp;       targetCompatibility = JavaVersion.VERSION\_1\_8

&nbsp;   }

&nbsp;   kotlinOptions {

&nbsp;       jvmTarget = "1.8"

&nbsp;   }

&nbsp;   buildFeatures {

&nbsp;       compose = true

&nbsp;   }

&nbsp;   composeOptions {

&nbsp;       kotlinCompilerExtensionVersion = "1.4.3"

&nbsp;   }

&nbsp;   packaging {

&nbsp;       resources {

&nbsp;           excludes += "/META-INF/{AL2.0,LGPL2.1}"

&nbsp;       }

&nbsp;   }

}



dependencies {



&nbsp;   implementation("androidx.core:core-ktx:1.9.0")

&nbsp;   implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")

&nbsp;   implementation("androidx.activity:activity-compose:1.10.0")

&nbsp;   implementation(platform("androidx.compose:compose-bom:2023.03.00"))



&nbsp;   implementation("androidx.compose.ui:ui")

&nbsp;   implementation("androidx.compose.ui:ui-graphics")

&nbsp;   implementation("androidx.compose.ui:ui-tooling-preview")



&nbsp;   implementation("androidx.compose.material3:material3")

&nbsp;   implementation("androidx.constraintlayout:constraintlayout:2.1.4")

&nbsp;   implementation("com.google.android.material:material:1.11.0")

&nbsp;   testImplementation("junit:junit:4.13.2")

&nbsp;   androidTestImplementation("androidx.test.ext:junit:1.1.5")

&nbsp;   androidTestImplementation("androidx.test.espresso:espresso-core:3.5.1")

&nbsp;   androidTestImplementation(platform("androidx.compose:compose-bom:2023.03.00"))

&nbsp;   androidTestImplementation("androidx.compose.ui:ui-test-junit4")

&nbsp;   debugImplementation("androidx.compose.ui:ui-tooling")

&nbsp;   debugImplementation("androidx.compose.ui:ui-test-manifest")



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

&nbsp;   override fun onCreate(savedInstanceState: Bundle?) {

&nbsp;       super.onCreate(savedInstanceState)

&nbsp;       setContent {

&nbsp;           HelloWorldScreen()

&nbsp;       }

&nbsp;   }

}

@Composable

fun HelloWorldScreen() {

&nbsp;   Column(

&nbsp;       modifier = Modifier

&nbsp;           .fillMaxSize()

&nbsp;           .padding(16.dp),

&nbsp;       horizontalAlignment = Alignment.CenterHorizontally,

&nbsp;       verticalArrangement = Arrangement.Center

&nbsp;   ){

&nbsp;       Text(

&nbsp;           text = "Hello World",

&nbsp;            style = MaterialTheme.typography.headlineLarge

&nbsp;       )

&nbsp;   }

}





2\. Configuring build.gradle.kts (Module:app)



Modify build.gradle.kts (Module: app) as follows:

plugins {

&nbsp;   id("com.android.application")

&nbsp;   id("org.jetbrains.kotlin.android")

}



android {

&nbsp;   namespace = "com.example.myapplication"

&nbsp;   compileSdk = 35



&nbsp;   defaultConfig {

&nbsp;       applicationId = "com.example.myapplication"

&nbsp;       minSdk = 24

&nbsp;       targetSdk = 35

&nbsp;       versionCode = 1

&nbsp;       versionName = "1.0"



&nbsp;       testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"

&nbsp;       vectorDrawables {

&nbsp;           useSupportLibrary = true

&nbsp;       }

&nbsp;   }



&nbsp;   buildTypes {

&nbsp;       release {

&nbsp;           isMinifyEnabled = false

&nbsp;           proguardFiles(

&nbsp;               getDefaultProguardFile("proguard-android-optimize.txt"),

&nbsp;               "proguard-rules.pro"

&nbsp;           )

&nbsp;       }

&nbsp;   }

&nbsp;   compileOptions {

&nbsp;       sourceCompatibility = JavaVersion.VERSION\_1\_8

&nbsp;       targetCompatibility = JavaVersion.VERSION\_1\_8

&nbsp;   }

&nbsp;   kotlinOptions {

&nbsp;       jvmTarget = "1.8"

&nbsp;   }

&nbsp;   buildFeatures {

&nbsp;       compose = true

&nbsp;   }

&nbsp;   composeOptions {

&nbsp;       kotlinCompilerExtensionVersion = "1.4.3"

&nbsp;   }

&nbsp;   packaging {

&nbsp;       resources {

&nbsp;           excludes += "/META-INF/{AL2.0,LGPL2.1}"

&nbsp;       }

&nbsp;   }

}



dependencies {



&nbsp;   implementation("androidx.core:core-ktx:1.9.0")

&nbsp;   implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.10.0")

&nbsp;   implementation("androidx.activity:activity-compose:1.10.0")

&nbsp;   implementation(platform("androidx.compose:compose-bom:2023.03.00"))

&nbsp;   implementation("androidx.compose.ui:ui")

&nbsp;   implementation("androidx.compose.ui:ui-graphics")

&nbsp;   implementation("androidx.compose.ui:ui-tooling-preview")

&nbsp;   implementation("androidx.compose.material3:material3")

&nbsp;   implementation("androidx.appcompat:appcompat:1.6.1")

&nbsp;   testImplementation("junit:junit:4.13.2")

&nbsp;   androidTestImplementation("androidx.test.ext:junit:1.3.0")

&nbsp;   androidTestImplementation("androidx.test.espresso:espresso-core:3.7.0")

&nbsp;   androidTestImplementation(platform("androidx.compose:compose-bom:2023.03.00"))

&nbsp;   androidTestImplementation("androidx.compose.ui:ui-test-junit4")

&nbsp;   debugImplementation("androidx.compose.ui:ui-tooling")

&nbsp;   debugImplementation("androidx.compose.ui:ui-test-manifest")

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

