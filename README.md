##  Chapter 1 homework for the DO288 bootcamp

Clone this git repo to your local disk and then use that to create a publicly visible git rep on github.com (the public one, not the IBM enterprise git repo).
It is possible to get this working from the IBM enterprise git repo, but that is a separate excercise. After this code is in the github.com repo, run the 
following instructions.

```
oc new-app --name=simple https://github.com/<your github.com id>/day3-simple-stuff.git
oc expose svc simple
oc patch route simple --type=json -p '[{"op": "add", "path": "/spec/tls", "value": {"termination": "edge"}}, {"op": "add", "path": "/spec/port", "value": {"targetPort": "9080-tcp"}}]'
```

And then, `curl -k https://<hostname for route>/simple-stuff/simple/simon`. This should produce the string "/my-special-folder does not exist"

## Task

0. Delete all existing artifiacts from the previous steps by running "oc delete all -l app=simple"

1. In the docker build, create a directory called /my-special-folder. Copy the Dockerfile in this git repo into that folder. Note that you will need to create this
folder as the root user, otherwise, your creation of the directory will fail during the build.
2. Repeat the new-app, expose, and patch commands provided at the top of this file.
3. Repeat steps 1 and 2, but this time, call the app "even-simpler".
4. Provide the output of the "curl" command shown above for the "simple" and "even-simpler" apps.
