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