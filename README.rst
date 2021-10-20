# helm-chart
Git repository (GitHub) with a sample Helm Chart
=============================================================

1. Create a helm chart from scratch
    - As a pre-requisite of this stage, you need to have the Helm CLI installed and initialized
    - I’m going to use the directory ./helm-chart-sources/ for the sources of our charts. I’m creating a default chart just for testing purposes, you might want to copy into ./helm-chart-sources/ your charts instead:

    $ mkdir ./helm-chart-sources && cd ./helm-chart-sources/
    $ helm create helm-chart-sources/helm-chart-test
    Creating helm-chart-sources/helm-chart-test

2. Lint the chart
    - As a good habit, helm lint runs a series of tests to verify that
    the chart is well-formed:

    $ helm lint helm-chart-sources/*

3. Create the Helm chart package
    - According to Helm:
        A repository is characterized primarily by the presence of a special file called index.yaml that has a list of all of the packages supplied by the repository, together with metadata that allows retrieving and verifying those packages.
    
    - So, everything we need to create is the index.yaml file and the command to do that is:
        $ helm repo index --url https://mattiaperi.github.io/helm-chart/ .
        $ cat index.yaml 
        apiVersion: v1
        entries:
        helm-chart-test:
        - apiVersion: v1
            appVersion: "1.0"
            created: 2019-04-16T11:10:08.729944+02:00
            description: A Helm chart for Kubernetes
            digest: 35a4e31bfacc496f1b1bce664652916bb8701cc9df77f1b90534f5234ff297a6
            name: helm-chart-test
            urls:
            - https://mattiaperi.github.io/helm-chart/helm-chart-test-0.1.0.tgz
            version: 0.1.0
        generated: 2019-04-16T11:10:08.729368+02:00

4. Configure the “helm-chart” repository as a Github pages site
    - Now it’s time to publish the contents of our git repository as Github pages. Go back to your browser, in the “settings” section of your git repository, scroll down to Github Pages section and configure it.

5. Configure helm client
    - In order to share your brand new repository, everyone interested in your charts need to configure their own Helm client. Also on client side, repositories are managed with the $ helm repo commands:
    $ helm repo add myhelmrepo https://mattiaperi.github.io/helm-chart/
    “myhelmrepo” has been added to your repositories

6. Test the Helm chart repository
    $ helm search test
    NAME CHART VERSION APP VERSION DESCRIPTION

myhelmrepo/helm-chart-test 0.1.0 1.0 A Helm chart for Kubernetes

7. Add new charts to an existing repository
    - Whenever you need to add a new chart to the Helm chart repository, it’s mandatory for you to regenerate the index.yaml file. The $ helm repo index command will completely rebuild the index.yaml file from scratch, including only the charts that it finds locally, which very likely is our case. However, it worth notice that you can use the --merge flag to incrementally add new charts to an existing index.yaml:
    $ helm repo index --url https://mattiaperi.github.io/helm-chart/ --merge index.yaml .

8. We can search for our repo:
    $ helm search repo helm-chart-test
    NAME                            CHART VERSION   APP VERSION     DESCRIPTION
    myhelmrepo/helm-chart-test      0.1.0           1.0             A Helm chart for Kubernetes

9. You get a simple idea of the features of this repo chart by running:
    $ helm show chart myhelmrepo/helm-chart-test
    Or you could run: - $ helm show all myhelmrepo/helm-chart-test to get all information about the chart.

10. We can install our helm chart repo with:
    - $ helm install myhelmrepo/helm-chart-test --generate-name
