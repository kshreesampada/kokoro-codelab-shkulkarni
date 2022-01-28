# kokoro-codelab-shkulkarni
# cd ~
# git clone https://github.com/kshreesampada/kokoro-codelab-shkulkarni.git
# cd kokoro-codelab-shkulkarni


public class Hello {
  public static void main(String[] argv) {
    System.out.println("Hello");
  }
}



#!/bin/bash

# Fail on any error.
set -e

# Display commands being run.
# WARNING: please only enable 'set -x' if necessary for debugging, and be very
#  careful if you handle credentials (e.g. from Keystore) with 'set -x':
#  statements like "export VAR=$(cat /tmp/keystore/credentials)" will result in
#  the credentials being printed in build logs.
#  Additionally, recursive invocation with credentials as command-line
#  parameters, will print the full command, with credentials, in the build logs.
# set -x

if [ "$1" == "release" ]; then
  javac -g:none Hello.java
else
  javac Hello.java
fi
java Hello




chmod +x build.sh
git add Hello.java
git add build.sh
git commit -m "Kokoro codelab prepwork"
git push origin main


