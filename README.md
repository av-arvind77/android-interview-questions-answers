# android-interview-questions-answers

## ANDROID

* <b> Activity/Fragment/Broadcast/Application/Service Lifecycle (Explain with one line description)</b> </br>
Ans : </br>
<b> Activity LifeCycle - </b> To navigate transitions between stages of the activity lifecycle, the Activity class provides a core set of six callbacks: onCreate(), onStart(),      onResume(), onPause(), onStop(), and onDestroy(). The system invokes each of these callbacks as an activity enters a new state. </br>
<b> Fragment LifeCycle - </b> Fragment Lifecycle in android mainly consists of these 8 methods : </br>
      1. onCreate()
      2. onCreateView()
      3. onStart
      4. onResume
      5. onPause
      6. onStop
      7. onDestroyView
      8. onDestroy </br>
<b> Braodcast Receiver - </b> Broadcast receiver is an Android component which allows you to send or receive Android system or application events. All the registered application are notified by the Android runtime once event happens. </br>
<b> Application - </b> The Application class in Android is the base class within an Android app that contains all other components such as activities and services. The Application class, or any subclass of the Application class, is instantiated before any other class when the process for your application/package is created.</br>
<b> Service - </b>  A Service is an application component that can perform long-running operations in the background. It does not provide a user interface. </br>

* <b>Which lifecycle method gets called when A goes to B/come back to A? Activity Launch Modes with examples</b>  </br>
Ans : </br>
First, it opened Activity A, where the following states are called initially, <b> onCreate -> onStart -> onResume </b> </br>
Then let's say on a click of a button we opened Activity B. While opening Activity B, first, <b>Pause</b> will be called for Activity A and then, <b> onCreate -> onStart -> onResume </b> will be called for Activity B. Then to finish this off, <b>onStop</b> of Activity A will be called and finally, Activity B would be loaded. </br>
Now, when we press the back button from Activity B to Activity A, then first,onPause of Activity B is called and then, <b> onRestart -> onStart -> onResume </b> gets called for Actvity A and it is displayed to the user. Here you can see <b>onRestart</b> gets called rather then <b>onCreate</b> as it is restarting the activity and not creating it. </b>
Then after <b>onResume</b> of Activity A is called then, <b>onStop -> onDestroy </b> is called for Activity B and hence the activity is destroyed   as the user has moved to Activtiy A. </br>

* <b>Let’s say 4 activities are there A->B->C->D. How to launch A from D finishing in between activities?</b> </br>
Ans :  finishAffinity() will finish the activities in between A and D.  </br>

* <b>How CLEAR_TOP flag intent works in android?</b> </br>
Ans : For CLEAR_TOP flag intent to work, you must change the launchMode of the Activity to anything other than standard. Otherwise it will be destroyed and recreated instead of being reset to the top.

* <b>Service vs IntentService?When to prefer which type of service? </b> </br>
Ans: 
  1. <b> Usage :</b> If you want some background task to be performed for a very long time then you should use the IntentService. But at the same time, you should take care that      there is no or very less communication with the main thread. If the communication is required then you can use main thread handler or broadcast intents. You can use service      for the tasks that don't require any UI and also it is not a very long running task.
  2. <b> How to start? :</b> To start a service you need to call the onStartService() method while in order to start a IntentService call, Context.startService(Intent)
  3. <b> Running Thread :</b> Service always runs on the Main thread while the IntentService runs on the separate Worker thread that is triggered from the main thread.
  4. <b> Triggering Thread :</b> Service can be triggered from any thread while the IntentService can be  triggered only from the Main thread i.e firstly , the Intent is               received on the Main thread and after that, the worker thread will be executed. 
  5. <b> Main Thread Blocking :</b> If you are using Service then there may be chance of Main thread blocking but IntentService there is no involvement of Main Thread.Here the         tasks are performed in the form of queue.
  6. <b> Stop Service :</b> If you are using Service then you have to stop the Service after using it otherwise Service will continue run an infinite period of time until phone       restarts but In case of IntentService, there is no stopping of Service because service will automatically stopped once work is done.
  7. <b> Interaction with UI :</b> If you are using IntentService, then you will find it difficult to interact with the UI of the application. If you want to out some result of      the IntentService in your UI, then you have to take help of some activity.

* <b>How to make a service persist even after Application killed? </b></br>
Ans : If your Service is started by your app then actually your service is running on main process. so when app is killed service will also be stopped. So what you can do is,        send broadcast from onTaskRemoved method of your service as follows: </br>
     Intent intent = new Intent("com.android.ServiceStopped"); </br>
     sendBroadcast(intent); </br>
     and have an broadcast receiver which will again start a service. I have tried it. service restarts from all type of kills.
     
* <b>How to achieve Interprocess communication in android? </b> </br>
Ans : IPC is inter-process communication. It describes the mechanisms used by different types of android components to communicate with one another.
      1) Intents are messages which components can send and receive. It is a universal mechanism of passing data between processes. With help of the intents one can start              services or activities, invoke broadcast receivers and so on.
      2) Bundles are entities of data that is passed through. It is similar to the serialization of an object, but much faster on android. Bundle can be read from intent via the        getExtras() method.
      3) Binders are the entities which allow activities and services to obtain a reference to another service. It allows not simply sending messages to services but directly          invoking methods on them.    

* <b>How Async task internally works? Async task implementation? </b> </br>
Ans : 
