# webview example for MinGW-w64 on Windows

MinGW-w64 distribution: https://winlibs.com/

Fetch dependencies:
```
cmd /c (if not exist libs\webview mkdir libs\webview) ^
    && curl -sSLo libs\webview\webview.h "https://raw.githubusercontent.com/webview/webview/master/webview.h"

cmd /c (if not exist libs\webview2 mkdir libs\webview2) ^
    && curl -sSL "https://www.nuget.org/api/v2/package/Microsoft.Web.WebView2" ^
    | tar -xf - -C libs\webview2
```

Build the example:
```cpp
if not exist bin mkdir bin
c++ -std=c++17 ^
    -Ilibs\webview ^
    -Ilibs\webview2\build\native\include ^
    src\main.cc ^
    -Llibs\webview2\build\native\x64 ^
    -lshlwapi -lole32 -lWebView2Loader.dll ^
    -o bin/main.exe
```

Copy third party libraries for convenience:
```
copy /Y libs\webview2\build\native\x64\WebView2Loader.dll bin
```

Now run `bin\main.exe` and see if it works.
