&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;!--

Licensed to the Apache Software Foundation \(ASF\) under one

or more contributor license agreements.  See the NOTICE file

distributed with this work for additional information

regarding copyright ownership.  The ASF licenses this file

to you under the Apache License, Version 2.0 \(the

"License"\); you may not use this file except in compliance

with the License.  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,

software distributed under the License is distributed on an

"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY

KIND, either express or implied.  See the License for the

specific language governing permissions and limitations

under the License.

--&gt;

&lt;!--

 \| This is the configuration file for Maven. It can be specified at two levels:

 \|

 \|  1. User Level. This settings.xml file provides configuration for a single user,

 \|                 and is normally provided in ${user.home}/.m2/settings.xml.

 \|

 \|                 NOTE: This location can be overridden with the CLI option:

 \|

 \|                 -s /path/to/user/settings.xml

 \|

 \|  2. Global Level. This settings.xml file provides configuration for all Maven

 \|                 users on a machine \(assuming they're all using the same Maven

 \|                 installation\). It's normally provided in

 \|                 ${maven.conf}/settings.xml.

 \|

 \|                 NOTE: This location can be overridden with the CLI option:

 \|

 \|                 -gs /path/to/global/settings.xml

 \|

 \| The sections in this sample file are intended to give you a running start at

 \| getting the most out of your Maven installation. Where appropriate, the default

 \| values \(values used when the setting is not specified\) are provided.

 \|

 \|--&gt;

&lt;settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"

          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd"&gt;

  &lt;!-- localRepository

   \| The path to the local repository maven will use to store artifacts.

   \|

   \| Default: ${user.home}/.m2/repository

  &lt;localRepository&gt;/path/to/local/repo&lt;/localRepository&gt;

  --&gt;

  &lt;localRepository&gt;D:\program\maven\repository&lt;/localRepository&gt;

    &lt;pluginGroups&gt;

  &lt;pluginGroup&gt;org.mortbay.jetty&lt;/pluginGroup&gt;

  &lt;/pluginGroups&gt;

  &lt;proxies&gt;&lt;/proxies&gt;

  &lt;servers&gt;

      &lt;server&gt;

      &lt;id&gt;nexus-releases&lt;/id&gt;

      &lt;username&gt;lbzxjy&lt;/username&gt;

      &lt;password&gt;nihao123!&lt;/password&gt;

    &lt;/server&gt;

    &lt;server&gt;

      &lt;id&gt;nexus-snapshots&lt;/id&gt;

      &lt;username&gt;lbzxjy&lt;/username&gt;

      &lt;password&gt;nihao123!&lt;/password&gt;

    &lt;/server&gt;

  &lt;/servers&gt;

  &lt;mirrors&gt; 

    &lt;mirror&gt; 

      &lt;id&gt;nexus&lt;/id&gt; 

      &lt;mirrorOf&gt;\*&lt;/mirrorOf&gt; 

      &lt;url&gt;http://nexus.dev.lbonline.cn/repository/maven-public&lt;/url&gt; 

    &lt;/mirror&gt;

  &lt;/mirrors&gt; 

  &lt;profiles&gt;

	&lt;profile&gt;

      &lt;id&gt;nexus&lt;/id&gt;

      &lt;repositories&gt;

        &lt;repository&gt;

          &lt;id&gt;maven-public&lt;/id&gt;

          &lt;url&gt;http://nexus.dev.lbonline.cn/repository/maven-public/&lt;/url&gt;

          &lt;releases&gt;&lt;enabled&gt;true&lt;/enabled&gt;&lt;/releases&gt;

          &lt;snapshots&gt;

			&lt;enabled&gt;true&lt;/enabled&gt;

			&lt;updatePolicy&gt;always&lt;/updatePolicy&gt;

		  &lt;/snapshots&gt;

        &lt;/repository&gt;

      &lt;/repositories&gt;

     &lt;pluginRepositories&gt;

        &lt;pluginRepository&gt;

          &lt;id&gt;maven-public&lt;/id&gt;

          &lt;url&gt;http://nexus.dev.lbonline.cn/repository/maven-public/&lt;/url&gt;

          &lt;releases&gt;&lt;enabled&gt;true&lt;/enabled&gt;&lt;/releases&gt;

          &lt;snapshots&gt;

			&lt;enabled&gt;true&lt;/enabled&gt;

			&lt;updatePolicy&gt;always&lt;/updatePolicy&gt;

		  &lt;/snapshots&gt;

        &lt;/pluginRepository&gt;

      &lt;/pluginRepositories&gt;

    &lt;/profile&gt;  

  &lt;/profiles&gt;

  &lt;activeProfiles&gt;

      &lt;activeProfile&gt;nexus&lt;/activeProfile&gt;

  &lt;/activeProfiles&gt;

&lt;/settings&gt;



