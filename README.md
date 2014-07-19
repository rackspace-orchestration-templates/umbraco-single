Description
===========

This is a template for deploying a Single Windows server running
[Umbraco](http://our.umbraco.org/documentation) on IIS,
ASP .Net 4.5 and with FTP enabled.

Requirements
============
* A Heat provider that supports `Rackspace::Cloud::WinServer`.
* An OpenStack username, password, and tenant id.
* [python-heatclient](https://github.com/openstack/python-heatclient)
`>= v0.2.8`:

```bash
pip install python-heatclient
```

We recommend installing the client within a [Python virtual
environment](http://www.virtualenv.org/).

Example Usage
=============
Here is an example of how to deploy this template using the
[python-heatclient](https://github.com/openstack/python-heatclient):

```
heat --os-username <OS-USERNAME> --os-password <OS-PASSWORD> --os-tenant-id \
  <TENANT-ID> --os-auth-url https://identity.api.rackspacecloud.com/v2.0/ \
  stack-create aspdotnet -f umbraco-app-single.yaml \
  -P server_hostname=my-site -P domain=example.org -P ftp_username=ftp_user
```

* For UK customers, use `https://lon.identity.api.rackspacecloud.com/v2.0/` as
the `--os-auth-url`.

Optionally, set environmental variables to avoid needing to provide these
values every time a call is made:

```
export OS_USERNAME=<USERNAME>
export OS_PASSWORD=<PASSWORD>
export OS_TENANT_ID=<TENANT-ID>
export OS_AUTH_URL=<AUTH-URL>
```

Parameters
==========
Parameters can be replaced with your own values when standing up a stack. Use
the `-P` flag to specify a custom parameter.

* `server_hostname`: Hostname to set for the server (Default: Umbraco)
* `image`: Operating System to use (Default: Windows Server 2008 R2 SP1)
* `flavor`: Server size for your deployment (Default: 4 GB Performance)

Outputs
=======
Once a stack comes online, use `heat output-list` to see all available outputs.
Use `heat output-show <OUTPUT NAME>` to get the value fo a specific output.

* `server_ip`: Public IP of the Windows server.
* `admin_password`: Administrator password for logging into the Windows Server.

Stack Details
=============
#### Getting Started
If you are new to Umbraco, the [Umbraco
Community](http://our.umbraco.org/forum) has great ressources to
get you started. The documentation is available [here](http://our.umbraco.org/documentation).
Umbraco provides [Training and Support](http://umbraco.com/help-and-support.aspx) and their
[Video Library](http://umbraco.com/help-and-support/video-tutorials/getting-started/what-is-umbraco) is very informative.

#### Logging into Umbraco
To login, use the IP address of the server or point an A record to your
server's IP. The domain you provided has also been used to set the [host
file](http://www.rackspace.com/knowledge_center/article/how-do-i-modify-my-hosts-file)
on the server. Therefore you can open a RDP session to the server,
open the domain in the web browser and pursue the last step of the Umbraco
site activation.

#### Additional Licensing
Umbraco is open source under the [MIT
Licence](http://umbraco.com/products/license).

#### Logging in via Remote Desktop
The Administrator password is included in the passwords/secrets section
of this deployment. Use that password and the instructions found
[here](http://www.rackspace.com/knowledge_center/article/logging-in-to-your-server-via-rdp-windows)
to login and begin managing Umbraco.

#### Uploading Files via FTP
The FTP password is included in the passwords/secrets section
of this deployment. You may use [Filezilla FTP Client](https://filezilla-project.org/)
or [Cyberduck](http://cyberduck.io/) with the FTP credential to upload your application.

#### Details of Your Setup
This setup was built through a [Powershell
Script](http://technet.microsoft.com/en-us/scriptcenter/dd742419.aspx).
Once the deployment is up, the script will not be run again, so it is
safe to change settings and configurations on your server and within
Umbraco.

#### Post Installation Permissions check
After the deployment, please verify Umbraco permissions check by opening
following the instruction on the following wiki
[article](http://our.umbraco.org/wiki/reference/files-and-folders/permissions/perform-permissions-check).

Contributing
============
There are substantial changes still happening within the [OpenStack
Heat](https://wiki.openstack.org/wiki/Heat) project. Template contribution
guidelines will be drafted in the near future.

License
=======
```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
