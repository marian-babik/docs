OSG Software Stack -- Data Release
==================================

**Release Date**: 2016-10-19

Summary of changes
------------------

This release contains:

-   CA Certificates based on [IGTF 1.78](http://dist.eugridpma.info/distribution/igtf/current/CHANGES)
    -   Removed superseded INFN-CA-2006 CA (IT)
    -   Updated Debian packaging to support APT security improvements
    -   Updated namespaces and signing\_policy files for CILogon Basic CA to permit DNs without "/C=US" (US)
    -   Added G2 series (sha-2) QuoVadis Root 2 and Grid ICA G2 (BM)
    -   Removed discontinued UniandesCA (CO)

This JIRA ticket ([SOFTWARE-2469](https://jira.opensciencegrid.org/browse/SOFTWARE-2469)) was addressed in this release.

Detailed changes are below. All of the documentation can be found in the [Release3](https://twiki.grid.iu.edu/bin/view/Documentation/Release3/) area of the TWiki.

Updating to the new release
---------------------------

### Update Repositories

To update to this series, you need [install the current OSG repositories](../../common/yum#install-osg-repositories).

### Update Software

Once the repositories are installed, you can update to this new release with:

``` console
root@host # yum update
```

<span class="twiki-macro NOTE"></span> Please be aware that running `yum update` may also update other RPMs. You can exclude packages from being updated using the `--exclude=[package-name or glob]` option for the `yum` command.

<span class="twiki-macro NOTE"></span> Watch the yum update carefully for any messages about a `.rpmnew` file being created. That means that a configuration file had been editted, and a new default version was to be installed. In that case, RPM does not overwrite the editted configuration file but instead installs the new version with a `.rpmnew` extension. You will need to merge any edits that have made into the `.rpmnew` file and then move the merged version into place (that is, without the `.rpmnew` extension). Watch especially for `/etc/lcmaps.db`, which every site is expected to edit.

Need help?
----------

Do you need help with this release? [Contact us for help](../../common/help).

Detailed changes in this release
--------------------------------

### Packages

We added or updated the following packages to the production OSG yum repository. Note that in some cases, there are multiple RPMs for each package. You can click on any given package to see the set of RPMs or see the complete list below.

#### Enterprise Linux 6

-   [igtf-ca-certs-1.78-1.osg33.el6](https://koji-hub.batlab.org/koji/search?match=glob&type=build&terms=igtf-ca-certs-1.78-1.osg33.el6)
-   [osg-ca-certs-1.58-1.osg33.el6](https://koji-hub.batlab.org/koji/search?match=glob&type=build&terms=osg-ca-certs-1.58-1.osg33.el6)

#### Enterprise Linux 7

-   [igtf-ca-certs-1.78-1.osg33.el7](https://koji-hub.batlab.org/koji/search?match=glob&type=build&terms=igtf-ca-certs-1.78-1.osg33.el7)
-   [osg-ca-certs-1.58-1.osg33.el7](https://koji-hub.batlab.org/koji/search?match=glob&type=build&terms=osg-ca-certs-1.58-1.osg33.el7)

### RPMs

If you wish to manually update your system, you can run yum update against the following packages:

    igtf-ca-certs osg-ca-certs

If you wish to only update the RPMs that changed, the set of RPMs is:

#### Enterprise Linux 6

``` file
igtf-ca-certs-1.78-1.osg33.el6
osg-ca-certs-1.58-1.osg33.el6
```

#### Enterprise Linux 7

``` file
igtf-ca-certs-1.78-1.osg33.el6
osg-ca-certs-1.58-1.osg33.el6
```

