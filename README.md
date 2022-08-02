A new standalone script to quickly check for CVE issues on customer's servers.
This will be added to CSI and eventually SSP (replacing the current method).

Default is to use a local copy of cve_data.json in the same directory as cvecheck.
If this file doesn't exist, then an attempt is made to download it from the CSI git repo.
You can pass the following options:

--help - what you see here!
--list - List the data within the cve_data.json file.
--verbose - Shows output of every thing checked. [ default is to be quiet ]
--debug - Show debug output of every thing checked. [ default is to be quiet ] --debug output may show errors.
--cvedata=local or --cvedata=remote - Use local file relative to cvecheck or download remote cve_data.json file.
--package=packagename - Check only this package against our cve_data.json file.
--cveid=CVE-XXXX-XXXXX - Check only this CVE ID against our cve_data.json file.

If nothing is returned when you run cvecheck, then your server should be patched and not vulnerable..

The steps performed  are:

    1) Is the package installed? (boolean true or false). If false, continue with next package.
    2) If true, then check if it's a kernel or linux-header package (boolean true or false).  kernel/linux-header packages require a name change to the package name.

    3) Check if the CVE ID from the known exploit is listed in the packages changelog (boolean true or false).
    4) If so, move on to the next package. If not, check the version of the installed package and see if it is greater than to the patched version.
    5) If so, then not vulnerable.  If not, then list it as possibly being vulnerable.

