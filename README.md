# ![Icon](./.bluemix/secure-lock-kubernetes.png) Secure Kubernetes with Helm Charts toolchain - deprecated
## use https://github.com/open-toolchain/simple-helm-toolchain instead

### Continuously deliver a secure Docker app to a Kubernetes Cluster with Helm Charts
This Hello World application uses Docker with Node.js and includes a DevOps toolchain that is preconfigured for continuous delivery across a staging and a prod Kubernetes cluster, with Vulnerability Advisor, source control, issue tracking, and online editing, and deployment to the IBM Bluemix Kubernetes Cluster using Helm Charts.

This template assumes an application (e.g. [hello-helm](https://github.com/open-toolchain/hello-helm)) structured like this  :
- **/Dockerfile (must)** -- the docker file used to build the container image in root folder
- **/chart /your-app-name  (must)** -- the Helm Chart used to deploy this application, CI pipeline will automatically update it to reflect latest image build
- **/scripts/build_image.sh (optional)** -- the custom container build script (if absent, will default to [generic script](https://github.com/open-toolchain/secure-helm-toolchain/blob/master/scripts/build_image.sh))
- **/scripts/check_vulnerabilities.sh (optional)** -- the custom vulnerability advisor script (if absent, will default to [generic script](https://github.com/open-toolchain/secure-helm-toolchain/blob/master/scripts/check_vulnerabilities.sh))
- **/scripts/deploy_helm.sh (optional)** -- the custom Kubernetes/Helm deploy script (if absent, will default to [generic script](https://github.com/open-toolchain/secure-helm-toolchain/blob/master/scripts/deploy_helm.sh))

It implements the following best practices:
- perform unit tests prior to building a container image (could be revisited to only occur after, or using a multistage build)
- sanity check the Dockerfile prior to attempting creating the image
- build container image once, and stage it through various Kubernetes environments (staging and prod, but could be further expanded by cloning pipeline stages)
- use a private image registry to store the built image, automatically configure access permissions for target cluster deployment using tokens than can be revoked
- check container image for security vulnerabilities
- use a Helm chart to conduct the deployment of each release
- use an explicit namespace in cluster to insulate each deployment (and make it easy to clear, by "kubectl delete namespace <name>")

![Icon](./.bluemix/toolchain.png)

### To get started, click this button:
[![Deploy To IBM Cloud](https://cloud.ibm.com/devops/graphics/create_toolchain_button.png)](https://cloud.ibm.com/devops/setup/deploy/?repository=https%3A//github.com/open-toolchain/secure-helm-toolchain)

---
### Learn more 

* TBD Blog [Continuously deliver your app to Kubernetes with Bluemix](https://www.ibm.com/blogs/bluemix/2017/07/continuously-deliver-your-app-to-kubernetes-with-bluemix/)
* TBD Step by step [tutorial](https://www.ibm.com/devops/method/tutorials/tc_secure_kube)
* [Getting started with IBM Cloud clusters](https://cloud.ibm.com/docs/containers?topic=containers-getting-started)
* [Getting started with toolchains](https://bluemix.net/devops/getting-started)
* [Documentation](https://cloud.ibm.com/docs/services/ContinuousDelivery?topic=ContinuousDelivery-getting-started&pos=2)

More links
* https://github.com/kubernetes/helm/blob/master/docs/charts_tips_and_tricks.md
* https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
* http://helm.readthedocs.io/en/latest/awesome/
* https://kubernetes.io/docs/concepts/containers/images/#using-a-private-registry
* https://www.ibm.com/blogs/bluemix/2017/03/whats-secret-pull-image-non-default-kubernetes-namespace-ibm-bluemix-container-service/
* https://cloud.ibm.com/docs/containers?topic=containers-images#cs_tutorials
* https://cloud.ibm.com/docs/containers?topic=containers-images#images
