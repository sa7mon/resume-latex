# Resume

## Compiling

- bring up docker compose project
- shell into sharelatex container
- 
    ```
    tlmgr update --self
    tlmgr install fontspec clearsans pstricks fontawesome textpos ragged2e etoolbox ifmtarg marvosym parskip pgf enumitem xkeyval booktabs caption
    apt update
    apt install texlive-fonts-extra
    apt install fonts-font-awesome
    ```

## Notes
* Compile using XeLaTeX

## 2025-08-25 Notes

Last time setting this up, used Overleaf Toolkit because the docker-compose project brought up with a user that I couldn't hack into with the reset URL. 

Overleaf Toolkit needed to be patched to get past the Mongo version check:

`lib/shared-functions.sh`

```diff
 function read_mongo_version() {
-  local mongo_image=$(read_configuration "MONGO_IMAGE")
-  local mongo_version=$(read_configuration "MONGO_VERSION")
+  local mongo_image="mongo"
+  echo $mongo_image
+  # local mongo_image=$(read_configuration "MONGO_IMAGE")
+  # local mongo_version=$(read_configuration "MONGO_VERSION")
+  local mongo_version="6.0"
+  echo $mongo_version
   if [ -z "${mongo_version}" ]; then
     if [[ "$mongo_image" =~ ^mongo:([0-9]+)\.(.*)$ ]]; then
       # when running a chain of commands (example: bin/up -> bin/docker-compose) we're passing
@@ -54,7 +58,7 @@ function read_mongo_version() {
       exit 1
     fi
   else
-    if [[ ! "$mongo_version" =~ ^([0-9]+)\.(.+)$ ]]; then
+    if [[ ! "$mongo_version" =~ ([0-9]+)\.(.+)$ ]]; then
```