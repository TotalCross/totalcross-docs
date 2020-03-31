---
description: Executing background tasks in order to not lock the Main Thread.
---

# Asynchronous Task

## Using AsyncTask class to execute background tasks 

In order to execute task that can take a few seconds to be completely executed, one must run it apart from the main thread, i.e, the thread responsible for painting components. Executing this kind of task in the main thread may cause a non-good user experience, once the application user may be unable to use and see any progress while the task is being executed. 

To avoid such an obstacle, TotalCross provides AsyncTask class, which is a helper to execute task in an asynchronous way. By using AsyncTask, the user can easily execute asynchronous task without complex manipulation of threads and, consequently, not locking the main thread. See the example bellow to learn how to use it.

{% hint style="info" %}
Copy and paste this code inside a [Container](control/container.md) instance.
{% endhint %}

```java
Button dldButton = new Button("download zip");
add(dldButton, CENTER, CENTER);

final ProgressBar progressBar = new ProgressBar();
add(progressBar, CENTER, AFTER + UnitsConverter.toPixels(DP + 16),
        PARENTSIZE + 80, PREFERRED);

dldButton.addPressListener((c) -> {
    new AsyncTask()<Void, Void, Void> {
        int progress = 0;
        UpdateListener updateListener = null;

        @Override
        protected Object doInBackground(Object... objects) {
            HttpStream.Options o = new HttpStream.Options();
            o.httpType = HttpStream.GET;
            final String url = "<INSERT AN URL TO DOWNLOAD A ZIP FILE>";

            if(url.startsWith("https:"))
                o.socketFactory = new SSLSocketFactory();

            try {
                HttpStream p = new HttpStream(new URI(url));
                File f = new File("file.zip", File.CREATE_EMPTY);
                int totalSize = p.contentLength;
                byte [] buff = new  byte[4096];
                BufferedStream bs = new BufferedStream(f, BufferedStream.WRITE, 4096);
                int counter = 0;
                while(true) {
                    int size = p.readBytes(buff, 0, buff.length);
                    counter += size;
                    progress = (int)((counter/(double)totalSize)*100);
                    if(size <= 0) break;
                    bs.writeBytes(buff, 0, size);
                }
                progress = 100;
                bs.close();
                p.close();
                f.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            return null;
        }

        @Override
        protected void onPreExecute() {
            dldButton.setEnabled(false);
            MainWindow.getMainWindow().addUpdateListener(updateListener = (elapsed) -> {
                progressBar.setValue(progress);
            });
        }

        @Override
        protected void onPostExecute(Object result) {
            dldButton.setEnabled(true);
            MainWindow.getMainWindow().removeUpdateListener(updateListener);
        }
    }.execute();
});
```

Once method execute is called, before executing the asynchronous task, _onPreExecute_ method is also called adding an _UpdateListener_ to update the component [`ProgressBar` ](../components/progress-bar.md)in the adequate time interval trough the variable _progress_. The button dldButton is disabled to avoid user execute the same task many times unnecessarily.  

When the file is completely downloaded, the function _onPostExecute_ is called removing the _UpdateListener_  and __reenabling __the button _dldButton._



