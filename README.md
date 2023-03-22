# ChartJsMigration

see https://jvanek.fedorapeople.org/charts/

this is keeping track of changes of migrating set of charts from chartjs1 to chartjs4. Original idea was to go version by version, but that proved to be nonsense, so the direct jump 1 to 4 was done, and only 4 is adapted.

chart4.js is not working, idk why. Use chart4-umd.js instead

First commit, adapting dataset to be accepted by chartjs 2 and up, is missing. But you can still get it by comapring chartjs1 against2 or other.. eg:
```
--- /home/jvanek/git/ChartJsMigration/charts/impl/index1.html
+++ /home/jvanek/git/ChartJsMigration/charts/impl/index2.html
@@ -1,10 +1,10 @@
 <!DOCTYPE html>
 <html>
-<script src="chartjs1/Chart.js" type="text/javascript"></script>
+<script src="chartjs2/Chart.js" type="text/javascript"></script>
 </head>
 
 <body>
-        <h6 onclick="document.getElementById('main').style.float='none'">click to don't see size issue</h6>
+        <h6 onclick="document.getElementById('main').style.float='none'">click to see size issue (then reload back)</h6>
         <div id="main" style="float:right">
                 <script type="text/javascript">var jckPassedChart = {}; var buildsMap = {};</script>
                 <h3 style="font-family: monospace">SPECjvm score (blacklisted 0) (whitelisted 0+0)</h3>
@@ -13,8 +13,10 @@
                 </div>
                 <script type="text/javascript">
                         // <![CDATA[
-                        var data = {
-                                labels: [
+                        var allPerf = {
+                                type: 'line',
+                                data: {
+                                        labels: [
 
                                                 "11.0.14.0.9-5.el8:100",
                                                 "11.0.14.0.9-6.el8:101",
@@ -78,13 +80,14 @@
                                                         ]
                                                 }
                                         ]
-                                };
-                                var options = {
+                                },
+                                options: {
                                         bezierCurve: false,
                                         multiTooltipTemplate: "<%= datasetLabel + \": \" + value %>"
+                                }
                         };
                         var ctx = document.getElementById("chart0").getContext("2d");
-                        jckPassedChart["chart0"] = new Chart(ctx).Line(data, options);
+                        jckPassedChart["chart0"] = new Chart(ctx, allPerf)
                         buildsMap["11.0.14.0.9-5.el8:100"] = "100"; buildsMap["11.0.14.0.9-6.el8:101"] = "101"; buildsMap["11.0.14.1.1-1.el8:102"] = "102"; buildsMap["11.0.14.1.1-4.el8:103"] = "103"; buildsMap["11.0.14.1.1-3.el8:104"] = "104"; buildsMap["11.0.14.1.1-5.el8:108"] = "108"; buildsMap["11.0.14.1.1-6.el8:111"] = "111"; buildsMap["11.0.15.0.10-3.el8:112"] = "112"; buildsMap["11.0.16.0.8-2.el8:113"] = "113"; buildsMap["11.0.16.1.1-2.el8:114"] = "114"; buildsMap["11.0.16.1.1-3.el8:115"] = "115"; buildsMap["11.0.17.0.8-2.el8:116"] = "116"; buildsMap["11.0.17.0.8-2.el8:117"] = "117"; buildsMap["11.0.18.0.9-0.3.ea.el8:118"] = "118"; buildsMap["11.0.18.0.10-3.el8:119"] = "119";
                         document.getElementById("chartContainer0").onclick = function (evt) {
                                 var activePoints = jckPassedChart["chart0"].getPointsAtEvent(evt);
@@ -99,7 +102,9 @@
                                         style="width: 500px; height: 500px;" width="500" height="500"></canvas></div>
                         <script type="text/javascript">
                                 // <![CDATA[
-                                        var data = {
+                                var allRpms = {
+                                        type: 'line',
+                                        data: {
                                                 labels: [
 
                                                         "1.8.0.332.b09-3.el7openjdkportable:37",
@@ -181,14 +186,15 @@
                                                                 ]
                                                         }
                                                 ]
-                                        };
-                                        var options = {
+                                        },
+                                        options: {
                                                 bezierCurve: false,
                                                 multiTooltipTemplate: "<%= datasetLabel + \": \" + value %>"
+                                        }
                                 };
                                 // Get the context of the canvas element we want to select
                                 var ctx = document.getElementById("rpmsChart-rpms").getContext("2d");
-                                diffChartClick["rpmsChart-rpms"] = new Chart(ctx).Line(data, options);
+                                diffChartClick["rpmsChart-rpms"] = new Chart(ctx, allRpms);
                                 diffBuildMap["1.8.0.332.b09-3.el7openjdkportable:37"] = "37"; diffBuildMap["1.8.0.332.b09-3.el7openjdkportable:38"] = "38"; diffBuildMap["1.8.0.342.b07-1.el7openjdkportable:39"] = "39"; diffBuildMap["1.8.0.345.b01-1.el7openjdkportable:41"] = "41"; diffBuildMap["1.8.0.352.b08-1.el7openjdkportable:43"] = "43"; diffBuildMap["1.8.0.362.b08-1.el7openjdkportable:46"] = "46"; diffBuildMap["1.8.0.362.b08-2.el7openjdkportable:47"] = "47"; diffBuildMap["1.8.0.362.b08-3.el7openjdkportable:48"] = "48"; diffBuildMap["1.8.0.362.b08-4.el7openjdkportable:49"] = "49"; diffBuildMap["1.8.0.362.b09-1.el7openjdkportable:50"] = "50";
                                 document.getElementById("rpmsChartContainer-rpms").onclick = function (evt) {
                                         var activePoints = diffChartClick["rpmsChart-rpms"].getPointsAtEvent(evt);
@@ -208,7 +214,9 @@
                                 style="width: 600px; height: 600px;" width="600" height="600"></canvas></div>
                 <script type="text/javascript">
                         // <![CDATA[
-                                var data = {
+                        var allJckFails = {
+                                type: 'line',
+                                data: {
                                         labels: [
 
                                                 "1.8.0.332.b09-3.el7openjdkportable:36",
@@ -268,13 +276,14 @@
                                                         ]
                                                 }
                                         ]
-                                };
-                                var options = {
+                                },
+                                options: {
                                         bezierCurve: false,
                                         multiTooltipTemplate: "<%= datasetLabel + \": \" + value %>"
-                                };
+                                }
+                        }
                         var ctx = document.getElementById("jckErrorsFailuresChart").getContext("2d");
-                        var jckErrorsChart = new Chart(ctx).Line(data, options);
+                        var jckErrorsChart = new Chart(ctx, allJckFails);
                         buildsMap["1.8.0.332.b09-3.el7openjdkportable:36"] = "36"; buildsMap["1.8.0.332.b09-3.el7openjdkportable:37"] = "37"; buildsMap["1.8.0.332.b09-3.el7openjdkportable:38"] = "38"; buildsMap["1.8.0.342.b07-1.el7openjdkportable:39"] = "39"; buildsMap["1.8.0.345.b01-1.el7openjdkportable:41"] = "41"; buildsMap["1.8.0.352.b08-1.el7openjdkportable:43"] = "43"; buildsMap["1.8.0.362.b08-2.el7openjdkportable:47"] = "47"; buildsMap["1.8.0.362.b08-3.el7openjdkportable:48"] = "48"; buildsMap["1.8.0.362.b08-4.el7openjdkportable:49"] = "49"; buildsMap["1.8.0.362.b09-1.el7openjdkportable:50"] = "50";
                         document.getElementById("jckErrorsFailuresChartContainer").onclick = function (evt) {
                                 var activePoints = jckErrorsChart.getPointsAtEvent(evt);
@@ -284,7 +293,9 @@
                 </script>
                 <script type="text/javascript">
                         // <![CDATA[
-                                var data = {
+                        var allJck = {
+                                type: 'line',
+                                data: {
                                         labels: [
 
                                                 "1.8.0.332.b09-3.el7openjdkportable:36",
@@ -344,13 +355,14 @@
                                                         ]
                                                 }
                                         ]
-                                };
-                                var options = {
+                                },
+                                options: {
                                         bezierCurve: false,
                                         multiTooltipTemplate: "<%= datasetLabel + \": \" + value %>"
+                                }
                         };
                         var ctx = document.getElementById("jckPassedChart").getContext("2d");
-                        var jckPassedChartTck = new Chart(ctx).Line(data, options);
+                        var jckPassedChartTck = new Chart(ctx, allJck);
                         buildsMap["1.8.0.332.b09-3.el7openjdkportable:36"] = "36"; buildsMap["1.8.0.332.b09-3.el7openjdkportable:37"] = "37"; buildsMap["1.8.0.332.b09-3.el7openjdkportable:38"] = "38"; buildsMap["1.8.0.342.b07-1.el7openjdkportable:39"] = "39"; buildsMap["1.8.0.345.b01-1.el7openjdkportable:41"] = "41"; buildsMap["1.8.0.352.b08-1.el7openjdkportable:43"] = "43"; buildsMap["1.8.0.362.b08-2.el7openjdkportable:47"] = "47"; buildsMap["1.8.0.362.b08-3.el7openjdkportable:48"] = "48"; buildsMap["1.8.0.362.b08-4.el7openjdkportable:49"] = "49"; buildsMap["1.8.0.362.b09-1.el7openjdkportable:50"] = "50";
                         document.getElementById("jckPassedChartContainer").onclick = function (evt) {
                                 var activePoints = jckPassedChartTck.getPointsAtEvent(evt);
@@ -360,7 +372,9 @@
                 </script>
                 <script type="text/javascript">
                         // <![CDATA[
-                                var data = {
+                        var allJckRegressions = {
+                                type: 'bar',
+                                data: {
                                         labels: [
 
                                                 "1.8.0.332.b09-3.el7openjdkportable:36",
@@ -416,13 +430,14 @@
                                                         ]
                                                 }
                                         ]
-                                };
-                                var options = {
+                                },
+                                options: {
                                         bezierCurve: false,
                                         multiTooltipTemplate: "<%= datasetLabel + \": \" + value %>"
+                                }
                         };
                         var ctx = document.getElementById("jckRegressionsChart").getContext("2d");
-                        var jckRegressions = new Chart(ctx).Bar(data, options);
+                        var jckRegressions = new Chart(ctx, allJckRegressions);
                         document.getElementById("jckRegressionsChartContainer").onclick = function (evt) {
                                 buildsMap["1.8.0.332.b09-3.el7openjdkportable:36"] = "36"; buildsMap["1.8.0.332.b09-3.el7openjdkportable:37"] = "37"; buildsMap["1.8.0.332.b09-3.el7openjdkportable:38"] = "38"; buildsMap["1.8.0.342.b07-1.el7openjdkportable:39"] = "39"; buildsMap["1.8.0.345.b01-1.el7openjdkportable:41"] = "41"; buildsMap["1.8.0.352.b08-1.el7openjdkportable:43"] = "43"; buildsMap["1.8.0.362.b08-2.el7openjdkportable:47"] = "47"; buildsMap["1.8.0.362.b08-3.el7openjdkportable:48"] = "48"; buildsMap["1.8.0.362.b08-4.el7openjdkportable:49"] = "49"; buildsMap["1.8.0.362.b09-1.el7openjdkportable:50"] = "50";
                                 var activePoints = jckRegressions.getBarsAtEvent(evt);

```
