OSG Site Administrator Documentation
====================================

Welcome to the home page of the Open Science Grid (OSG) Site Administrator documentation! If you are not a site adminstrator...

- If you are a researcher interested in using OSG resources, you can find user documentation [here](https://support.opensciencegrid.org/support/home). 
- If you'd like to learn more about the OSG and our mission, visit our website [here](https://www.opensciencegrid.org/).

This document outlines the overall installation process for an OSG site and provides many links into detailed installation, configuration, troubleshooting, and similar pages. If you do not see software-related technical documentation listed here, try the search bar to the left or contacting us at [goc@opensciencegrid.org](mailto:goc@opensciencegrid.org).

Plan the Site
-------------

If you have not done so already, [plan the overall architecture of your OSG site](site-planning). It is recommended that your plan be sufficiently detailed to include the OSG hosts that are needed and the main software components for each host. Be sure to consider [the operating systems that OSG supports](https://twiki.opensciencegrid.org/bin/view/Documentation/Release3/SupportedOperatingSystems). For example, a basic site might include:

| Purpose              | Host                                | Major Software                                           |
|:---------------------|:------------------------------------|:---------------------------------------------------------|
| Compute Element (CE) | `osg-ce.example.edu`                | OSG CE, HTCondor Central Manager, etc. (`osg-ce-condor`) |
| Worker Nodes         | `wNNN.cluster.example.edu`          | OSG worker node client (`osg-wn-client`)                 |

Prepare the Batch System
------------------------

The assumption is that you have an existing batch system at your site. Currently, we support [HTCondor](http://research.cs.wisc.edu/htcondor/), [LSF](http://www-03.ibm.com/systems/platformcomputing/products/lsf/), [PBS](http://www.pbsworks.com) and [TORQUE](http://www.adaptivecomputing.com/products/open-source/torque/), [SGE](http://en.wikipedia.org/wiki/Oracle_Grid_Engine), and [Slurm](http://slurm.schedmd.com) batch systems.

For smaller sites (less than 50 worker nodes), the most common way to add a site to OSG is to install the OSG Compute Element (CE) on the central host of your batch system.  At such a site - especially if you have minimal time to maintain a CE - you may want to contact <mailto:goc@opensciencegrid.org> to ask about using an OSG-hosted CE instead of running your own.  Before proceeding with an install, be sure that you can submit and successfully run a job from your OSG CE host into your batch system.

Add OSG Software
----------------

If necessary, provision all OSG hosts that are in your site plan and that do not exist yet.

!!! note
    For sites with more than a handful of worker nodes, it is recommended to use some sort of configuration management tool to install, configure, and maintain your site. While beyond the scope of OSG’s documentation to explain how to select and use such a system, some popular configuration management tools are [Puppet](http://puppetlabs.com), [Chef](https://www.chef.io), [Ansible](https://www.ansible.com), and [CFEngine](http://cfengine.com).

### General Installation Instructions ###


-   [Security information for OSG signed RPMs](release/signing)
-   [Using Yum and RPM](release/yum-basics)
-   [Install the OSG repositories](common/yum)
-   [OSG Software release series](release/release_series) - look here to upgrade from OSG 3.1 to OSG 3.2 or from OSG 3.2 to OSG 3.3
-   [Installation best practices](common/install-best-practices)

### Installing and Managing Certificates for Site Security ###

-   [Installing the grid certificate authorities (CAs)](common/ca)
-   [How do I get PKI host and service X.509 certificates?](security/host-certs)
-   [Automatically updating the grid certificate authorities (CAs)](common/osg-ca-certs-updater)
-   [SHA-2 certificates and minimum required OSG software versions](https://twiki.opensciencegrid.org/bin/view/Documentation/Release3/SHA2Compliance)
-   [OSG PKI command line client reference](common/pki-cli)

### Adding OSG Software to Worker Nodes ###

-   [Worker Node (WN) Client Overview](worker-node/using-wn)
-   Install the WN client software on every worker node – pick a method:
    -   [Using RPMs](worker-node/install-wn) – useful when managing your worker nodes with a tool (e.g., Puppet, Chef)
    -   [Using a tarball](worker-node/install-wn-tarball) – useful for installation onto a shared filesystem (does not require root access)
    -   [Using OASIS](worker-node/install-wn-oasis) – useful when [CVMFS](worker-node/install-cvmfs) is already mounted on your worker nodes
-   (optional) [Install the CernVM-FS client](worker-node/install-cvmfs) to make it easy for user jobs to use needed software from OSG's OASIS repositories
-   (optional) [Install singularity on the OSG worker node](worker-node/install-singularity), to allow pilot jobs to isolate user jobs.

### Installing and Configuring the Compute Element ###

-   [Preparing to install the compute element](https://twiki.opensciencegrid.org/bin/view/Documentation/Release3/PreparingComputeElement)
-   Install the compute element (HTCondor-CE and other software):
    -   [Overview and architecture](compute-element/htcondor-ce-overview)
    -   [Install HTCondor-CE](compute-element/install-htcondor-ce)
    -   [Configure the HTCondor-CE job router](compute-element/job-router-recipes), including common recipes
    -   [Troubleshooting HTCondor-CE installations](compute-element/troubleshoot-htcondor-ce)
    -   [Submitting jobs to HTCondor-CE](compute-element/submit-htcondor-ce)
-   [Troubleshooting osg-configure](https://twiki.opensciencegrid.org/bin/view/Documentation/Release3/TroubleshootingOsgConfigure)

### Installing and Configuring Other Nodes ###

All of these node types and their services are optional, although OSG requires the Frontier Squid caching service if you have installed [CVMFS](worker-node/install-cvmfs) on your worker nodes.

-   [Install Frontier Squid, the HTTP caching proxy service](data/frontier-squid)
-   RSV monitoring to monitor and report to OSG on the health of your site
    -   [Install RSV](monitoring/install-rsv)
    -   [Troubleshooting RSV](https://twiki.opensciencegrid.org/bin/view/Documentation/Release3/TroubleshootRsv)
-   [Install the GlideinWMS VO Frontend](other/install-gwms-frontend) if your want your users’ jobs to run on the OSG
    -   [Install the RSV GlideinWMS Tester](monitoring/install-rsv-gwms-tester) if you want to test your front-end's ability to submit jobs to sites in the OSG
-   Storage element (pick one):
    -   GridFTP
        -   [Install standalone OSG GridFTP](data/gridftp): GridFTP server
        -   (optional) [Install load-balanced OSG GridFTP](data/load-balanced-gridftp): when a single GridFTP server isn't enough
    -   BeStMan
        -   [Install Bestman SE](data/bestman-install): BeStMan2 SRM server + GridFTP server
        -   [Install Bestman Gateway Hadoop](https://twiki.opensciencegrid.org/bin/view/Documentation/Release3/InstallHadoop200SE): BeStMan2 SRM server + GridFTP server + Hadoop
    -   Hadoop Distributed File System (HDFS)
        -   [Hadoop Overview](https://twiki.opensciencegrid.org/bin/view/Documentation/Release3/HadoopOverview): HDFS information, planning, and guides
    -   XRootD
        -   [XRootd Overview](data/xrootd-overview): XRootD information, planning, and guides
        -   [Install Xrootd Server](https://twiki.opensciencegrid.org/bin/view/Documentation/Release3/InstallXrootd): XRootD redirector installation
        -   [Install BeStMan-Gateway XRootD](data/install-bestman-xrootd): BeStMan2 SRM server + GridFTP server + XRootD fuse

Test OSG Software
-----------------

At very least, it is vital to test *manual* submission of jobs from inside and outside of your site through your CE to your batch system. If this process does not work manually, it will probably not work for the glideinWMS pilot factory either.

-   [Test job submission into an HTCondor-CE](compute-element/submit-htcondor-ce)

Start GlideinWMS Pilot Submissions
----------------------------------

To begin running [GlideinWMS](http://www.uscms.org/SoftwareComputing/Grid/WMS/glideinWMS/) pilot jobs at your site, e-mail <osg-gfactory-support@physics.ucsd.edu> and tell them that you want to start accepting Glideins. Please provide them with the following information:

-   The type of CE (HTCondor-CE or the now-unsupported GRAM-CE)
-   The fully qualified hostname of the CE
-   Resource/WLCG name
-   OS major version of your worker nodes — EL 6, EL 7, or a mix of both?
-   Do you accept multicore jobs?
-   Maximum job walltime
-   Maximum job memory usage

Once the factory team has enough information, they will start submitting pilots from the test factory to your CE. Initially, this will be one pilot at a time but once the factory verifies that pilot jobs are running successfully, that number will be ramped up to 10, then 100.

Verify Reporting and Monitoring
-------------------------------

To verify that your site is correctly reporting to the OSG, check [OSG's Accounting Portal](https://gracc.opensciencegrid.org/dashboard/db/site-summary) for records of your site reports (select your site from the drop-down box). If you have enabled the OSG VO, you can also check <http://osg-flock.grid.iu.edu/monitoring/condor/sites/all_1day.html>.

Scale Up Site to Full Production
--------------------------------

After successfully running all the pilot jobs that are submitted by the test factory and verifying your site reports, your site will be deemed production ready. No action is required on your end, factory operations will start submitting pilot jobs from the production factory.
