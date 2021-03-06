---
title: "Deployments"
date: 2019-06-18T16:42:20+02:00
lastmod: 2019-06-18T16:42:20+02:00
publishdate: 2019-06-18T16:42:20+02:00
draft: false
weight: 16
---

# Import environment variables from a file

(via https://twitter.com/kamesh_sampath/status/1179984908690739201)

Instead modifying the deployment, you can create an environment variables file
such as `myvars.env`:

```
MYSQL_DB="mysql"
MYSQL_DBPORT="3306"
OTHERVAR="foo"
```

Then:

```
cat myvars.env | oc set env -e - deployment/mydeployment -n mynamespace
```

# Set some of the local shell environment into a deployment config

```
env | grep MYSQL_ | oc set env -e - deployment/mydeployment -n mynamespace
```

# Import environment variables from a configmap with a prefix

```
oc set env --from=configmap/myconfigmap --prefix=MYSQL_ deployment/mydeployment -n mynamespace
```

# Import specific keys from a configmap

```
oc set env --from=configmap/myconfigmap --keys=OTHERVAR deployment/mydeployment -n mynamespace
```

# Remove environment variable in a deployment

```
oc set env -e OTHERVAR- deployment/mydeployment -n mynamespace
```

# Remove environment variable from container 'c1' in a deployment

```
oc set env deployment/mydeployment --containers="c1" OTHERVAR-
```

# Remove environment variable from container 'c1' in all deployments

```
oc set env deployments --all --containers="c1" OTHERVAR-
```
