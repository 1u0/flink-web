---
title:  "How To Contribute"
layout: with_toc
---

The Flink project welcomes all sorts contributions in the form of code (improvements, features, bugfixes), documentation, tests, and community participation (discussions & questions).



## Easy Issues for Starters

We maintain all known issues and feature drafts in the [Flink project JIRA](https://issues.apache.org/jira/issues/?jql=project+%3D+FLINK).

We also try to maintain a <a href="https://issues.apache.org/jira/browse/FLINK-992?jql=project%20%3D%20FLINK%20AND%20labels%20%3D%20starter%20AND%20status%20in%20(Open%2C%20Reopened)">list of simple "starter issues"</a> that we believe are good tasks for new contributors. Those tasks are meant to allow people to get into the project and become familiar with the process of contributing. Feel free to ask questions about issues that you would be interested in working on.

In addition, you can find a list of ideas for projects and improvements in the [projects wiki page](https://cwiki.apache.org/confluence/display/FLINK/Project+Ideas).



## Contributing Code & Documentation

This section gives you a brief introduction in how to contribute code and documentation to Flink. We maintain both the code and the documentation in the same repository, so the process is essentially the same for both. We use [git](http://git-scm.com/) for the code and documentation version control. The documentation is located in the `docs/` subdirectory of the git repository.

The Flink project accepts code contributions though the [GitHub Mirror](https://github.com/apache/incubator-flink), in the form of [Pull Requests](https://help.github.com/articles/using-pull-requests). Pull requests are basically a simpler way of offering a patch, by providing a pointer to a code branch that contains the change. 

It is also possible to attach a patch to a [JIRA]({{site.FLINK_ISSUES_URL}}) issue.


### Setting up the Infrastructure and Creating a Pull Request

1. The first step is to create yourself a copy of the Flink code base. We suggest to fork the [Flink GitHub Mirror Repository](https://github.com/apache/incubator-flink) into your own [GitHub](https://github.com) account. You need to register on GitHub for that, if you have no account so far.

2. Next, clone your repository fork to your local machine.
```
git clone https://github.com/<your-user-name>/incubator-flink.git
```

3. It is typically helpful to switch to a *topic branch* for the changes. To create a dedicated branch based on the current master, use the following command:
```
git checkout -b myBranch master
```

4. Now you can create your changes, compile the code, and validate the changes. Here are some pointers on how to [build the code](https://github.com/apache/incubator-flink/#build-apache-flink).
In addition to that, we recommend setting up Eclipse (or IntelliJ) using the "Import Maven Project" feature. If you want to work on the scala code you will need the following plugins:

    Eclipse 4.x:
      * scala-ide: http://download.scala-ide.org/sdk/e38/scala210/stable/site
      * m2eclipse-scala: http://alchim31.free.fr/m2e-scala/update-site
      * build-helper-maven-plugin: https://repository.sonatype.org/content/repositories/forge-sites/m2e-extras/0.15.0/N/0.15.0.201206251206/

    Eclipse 3.7:
      * scala-ide: http://download.scala-ide.org/sdk/e37/scala210/stable/site
      * m2eclipse-scala: http://alchim31.free.fr/m2e-scala/update-site
      * build-helper-maven-plugin: https://repository.sonatype.org/content/repositories/forge-sites/m2e-extras/0.14.0/N/0.14.0.201109282148/

    When you don't have the plugins your project will have build errors, you can just close the scala projects and ignore them.

    Import the Flink source code using Maven's Import tool:
      * Select "Import" from the "File"-menu.
      * Expand "Maven" node, select "Existing Maven Projects", and click "next" button
      * Select the root directory by clicking on the "Browse" button and navigate to the top folder of the cloned Flink git repository.
      * Ensure that all projects are selected and click the "Finish" button.

5. After you have finalized your contribution, verify the compliance with the contribution guidelines (see below), and commit them. To make the changes easily mergeable, please rebase them to the latest version of the main repositories master branch. Assuming you created a topic branch (step 3), you can follow this sequence of commands to do that:
Switch to the master branch, update it to the latest revision, switch back to your topic branch, and rebase it on top of the master branch.
```
git checkout master
git pull https://github.com/apache/incubator-flink.git master
git checkout myBranch
git rebase master
```
Have a look [here](https://help.github.com/articles/using-git-rebase) for more information about rebasing commits.


6. Push the contribution it back into your fork of the Flink repository.
```
git push origin myBranch
```
Go the website of your repository fork (`https://github.com/<your-user-name>/incubator-flink`) and use the "Create Pull Request" button to start creating a pull request. Make sure that the base fork is `apache/incubator-flink master` and the head fork selects the branch with your changes. Give the pull request a meaningful description and send it.


### Verifying the Compliance of your Code

Before sending a patch or pull request, please verify that it complies with the guidelines of the project. While we try to keep the set of guidelines small and easy, it is important to follow those rules in order to guarantee good code quality, to allow efficient reviews, and to allow committers to easily merge your changes.

Please have a look at the [coding guidelines]({{ site.baseurl }}/docs/{{ site.FLINK_CURRENT_DOCUMENTATION }}/coding_guidelines.html) for a guide to the format of code and pull requests.

Most important of all, verify that your changes are correct and do not break existing functionality. Run the existing tests by calling `mvn verify` in the root directory of the repository, and make sure that the tests succeed. We encourage every contributor to use a *continuous integration* service that will automatically test the code in your repository whenever you push a change. Flink is pre-configured for [Travis CI](http://docs.travis-ci.com/), which can be easily enabled for your private repository fork (it uses GitHub for authentication, so you so not need an additional account). Simply add the *Travis CI* hook to your repository (*settings --> webhooks & services --> add service*) and enable tests for the "incubator-flink" repository on [Travis](https://travis-ci.org/profile).

When contributing documentation, please review the rendered HTML versions of the documents you changed. You can look at the HTML pages by using the rendering script in preview mode. 
```
cd docs
./build_docs.sh -p
```
Now, open your browser at `http://localhost:4000` and check out the pages you changed.

## Contribute changes to the Website

The website of Apache Flink is hosted in a [Subversion (SVN)](https://subversion.apache.org/) repository. The repository is located here: [https://svn.apache.org/repos/asf/flink/](https://svn.apache.org/repos/asf/flink/).

To make changes to the website, you have to checkout the source code of it first:
```
svn checkout https://svn.apache.org/repos/asf/incubator/flink/
cd flink
```

The `flink` repository contains the files that we use to build the website. We use [Jekyll](http://jekyllrb.com/) to generate static HTML files for the website. 

### Files and Directories in the SVN repository

The files and directories in the SVN repository have the following roles:
- all files ending with `.md` are [Markdown](http://daringfireball.net/projects/markdown/) files. Those are the input for the HTML files.
- regular directories (not starting with an underscore (`_`)) contain also `.md` files. The directory structure is also represented in the generated HTML files.
- the `_posts` directory contains one Markdown file for each blog post on the website. To contribute a post, just add a new file there.
- the `_includes/` directory contains includeable files such as the navigation bar or the footer.
- the `docs/` directory contains copies of the documentation of Flink for different releases. There is a directory inside `docs/` for each stable release and the latest SNAPSHOT version. The build script is taking care of the maintenance of this directory.
- the `site/` directory contains the generated HTML files from Jekyll. It is important to place the files in this directory since the Apache Infrastructure to host the Flink website is pulling the HTML content from his directory. (For committers: When pushing changes to the website svn, push also the updates in the `site/` directory!)
- see the section below for he `build.sh` script


### The `build.sh` script

The `build.sh` script creates HTML files from the input Markdown files. Use the `-p` flag to let Jekyll serve a **p**review of the website on http://localhost:4000/.

The build script also takes care of maintaining the `docs/` directory. Set the `-u` flag to **u**pdate documentation. This includes fetching the Flink git repository and copying different versions of the documentation.

### Submit a patch

To contribute back your changes to the main project, create a patch that you can attach to a JIRA issue.

```
svn diff > improvement.patch
```
Upload the `.patch` file to a JIRA issue.

## How to become a committer

There is no strict protocol for becoming a committer. Candidates for new committers are typically people that are active contributors and community members.

Being an active community member means participating on mailing list discussions, helping to answer questions, being respectful towards others, and following the meritocratic principles of community management. Since the "Apache Way" has a strong focus on the project community, this part is very important.

Of course, contributing code to the project is important as well. A good way to start is contributing improvements, new features, or bugfixes. You need to show that you take responsibility for the code that you contribute, add tests/documentation, and help maintaining it. 

Finally, candidates for new committers are suggested by current committers, mentors, or PMC members, and voted upon by the PMC.


### How to use git as a committer

Only the infrastructure team of the ASF has administrative access to the GitHub mirror. Therefore, comitters have to push changes to the git repository at the ASF.

**ASF writable git**: [https://git-wip-us.apache.org/repos/asf/incubator-flink.git](https://git-wip-us.apache.org/repos/asf/incubator-flink.git)

**ASF read-only git**: [http://git-wip-us.apache.org/repos/asf/incubator-flink.git](http://git-wip-us.apache.org/repos/asf/incubator-flink.git)

**ASF git web interface**: [https://git-wip-us.apache.org/repos/asf?p=incubator-flink.git;a=summary](https://git-wip-us.apache.org/repos/asf?p=incubator-flink.git;a=summary)

**ASF svn for the website**: [https://svn.apache.org/repos/asf/incubator/flink/](https://svn.apache.org/repos/asf/incubator/flink/).

Details on how to set the credentials for the ASF git repostiory are [linked here](https://git-wip-us.apache.org/).
To merge pull requests from our GitHub mirror, there is a script in the source `./tools/merge_pull_request.sh.template`. Rename it to `merge_pull_request.sh` with the appropriate settings and use it for merging.