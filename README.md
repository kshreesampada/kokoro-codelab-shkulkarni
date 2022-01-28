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


cd ~/kokoro-codelab-shkulkarni
mkdir -p kokoro/gcp_ubuntu

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

# Code under repo is checked out to ${KOKORO_ARTIFACTS_DIR}/github.
# The final directory name in this path is determined by the scm name specified
# in the job configuration.
cd "${KOKORO_ARTIFACTS_DIR}/github/kokoro-codelab-shkulkarni"
./build.sh


chmod +x kokoro/gcp_ubuntu/kokoro_build.sh


# -*- protobuffer -*-
# proto-file: google3/devtools/kokoro/config/proto/build.proto
# proto-message: BuildConfig

# Location of the bash script. Should have value <github_scm.name>/<path_from_repository_root>.
# github_scm.name is specified in the job configuration (next section).
build_file: "kokoro-codelab-shkulkarni/kokoro/gcp_ubuntu/kokoro_build.sh"

# -*- protobuffer -*-
# proto-file: google3/devtools/kokoro/config/proto/build.proto
# proto-message: BuildConfig

# Location of the bash script. Should have value <github_scm.name>/<path_from_repository_root>.
# github_scm.name is specified in the job configuration (next section).
build_file: "kokoro-codelab-shkulkarni/kokoro/gcp_ubuntu/kokoro_build.sh"


git add -A
git commit -m "Kokoro codelab build config and scripts"
git push origin main

g4d -f kokoro-codelab-shkulkarni
mkdir experimental/kokoro/config/qa/codelab/shkulkarni
echo shkulkarni >> experimental/kokoro/config/qa/codelab/shkulkarni/OWNERS

# -*- protobuffer -*-
# proto-file: google3/devtools/kokoro/config/proto/job.proto
# proto-message: JobConfig

admins {
  sso_user: "shkulkarni"
}
email_to: "shkulkarni@google.com"


mkdir -p experimental/kokoro/config/qa/codelab/shkulkarni/gcp_ubuntu

# -*- protobuffer -*-
# proto-file: google3/devtools/kokoro/config/proto/job.proto
# proto-message: JobConfig

# Build on the GCP_UBUNTU cluster.
cluster: GCP_UBUNTU
pool: "dynamic"

multi_scm {
  github_scm {
    # Owner of the repository.
    owner: "kshreesampada
    "
    # GitHub repository name.
    repository: "kokoro-codelab-shkulkarni"
    # Sources will be cloned into a directory named
    # ${KOKORO_ARTIFACTS_DIR}/github/[this value]
    name: "kokoro-codelab-shkulkarni"
    # Name of the branch to poll for presubmit/continuous builds.
    branch: "main"
    # Group whose actions can auto-trigger presubmit builds.
    # For the sake of codelabs, set COLLABORATOR so you just need to be
    # a collaborator on the repository.
    # The default is ORGANIZATION_MEMBER which requires that users be public
    # members of the repository's organization
    authorized_group: COLLABORATOR
  }
  # Where build configs live. You need to prefix the path with github_scm.name.
  build_config_dir: "kokoro-codelab-shkulkarni/kokoro/gcp_ubuntu"
}


# -*- protobuffer -*-
# proto-file: google3/devtools/kokoro/config/proto/job.proto
# proto-message: JobConfig

type: CONTINUOUS_INTEGRATION

# -*- protobuffer -*-
# proto-file: google3/devtools/kokoro/config/proto/job.proto
# proto-message: JobConfig

type: PRESUBMIT_GITHUB

g4d kokoro-codelab-shkulkarni
g4 reopen -Ra
g4 submit --desc "Kokoro codelab job config"

  
