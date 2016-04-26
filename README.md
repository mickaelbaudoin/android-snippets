# android-snippets
snippets android

## catch all exception

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
## websocket
## service not killed
