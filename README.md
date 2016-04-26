# android-snippets
snippets android

## Logger with log4j

#### 1] Dependencies  
- compile 'de.mindpipe.android:android-logging-log4j:1.0.2'
- compile 'log4j:log4j:1.2.17'

#### 2] Configurator
<pre>
public class Configurator {

    public static org.apache.log4j.Logger getLogger(Class clazz) {
        final LogConfigurator logConfigurator = new LogConfigurator();
        logConfigurator.setFileName(Environment.getExternalStorageDirectory().toString() + File.separator + "log/visio-mobile.log");
        logConfigurator.setRootLevel(Level.ALL);
        logConfigurator.setLevel("org.apache", Level.ALL);
        logConfigurator.setUseFileAppender(true);
        logConfigurator.setFilePattern("%d %-5p [%c{2}]-[%L] %m%n");
        logConfigurator.setMaxFileSize(1024 * 1024 * 5);
        logConfigurator.setImmediateFlush(true);
        logConfigurator.configure();
        Logger log = Logger.getLogger(clazz);
        return log;
    }

}
</pre>

#### 3] Instance logger
<pre>
protected org.apache.log4j.Logger logger = Configurator.getLogger(myClass.class);
</pre>

## Catch all exception

<pre>
    Thread.setDefaultUncaughtExceptionHandler (new Thread.UncaughtExceptionHandler()
    {
        @Override
        public void uncaughtException (Thread thread, Throwable e)
        {
            handleUncaughtException (thread, e);
        }
    });

    protected void handleUncaughtException (Thread thread, Throwable e)
    {
        //On log l'erreur
        String tag = getApplicationContext().getClass().getName();
        logger.error(e.getStackTrace().toString());
        logger.error(e.getMessage());

        System.exit(1);
    }
</pre>
## Websocket
## Service not killed

Trigger alarm system repeat

<pre>
    private void triggerAlarmRepeat(){
        Calendar cal = Calendar.getInstance();

        Intent intent = new Intent(this, CheckNotificationServerEvent.class);
        PendingIntent pintent = PendingIntent.getService(this, 0, intent, 0);

        AlarmManager alarm = (AlarmManager)getSystemService(Context.ALARM_SERVICE);
        // Start every minute
        alarm.setRepeating(AlarmManager.RTC_WAKEUP, cal.getTimeInMillis(), 60 * 1000, pintent);
    }
</pre>
