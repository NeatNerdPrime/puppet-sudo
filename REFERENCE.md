# Reference

<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

### Classes

#### Public Classes

* [`sudo`](#sudo): This module manages sudo
* [`sudo::allow`](#sudo--allow): Creates a file in sudoers.d that permits specific users and groups to sudo.

#### Private Classes

* `sudo::package`: Installs the sudo package on various platforms.
* `sudo::package::aix`: Install the perzl.org sudo package. It also requires the openldap
rpm. so we add a dependencies to the ldap module.
* `sudo::package::solaris`: install sudo under solaris 10/11.
* `sudo::params`: Params class for the sudo module

### Defined types

* [`sudo::conf`](#sudo--conf): Manages sudo configuration snippets

### Functions

* [`sudo::defaults`](#sudo--defaults): Formats sudoers defaults config see https://linux.die.net/man/5/sudoers      Default_Type ::= 'Defaults' |                      'Defaults' '@

### Data types

* [`Sudo::Defaults`](#Sudo--Defaults): sudo defaults
* [`Sudo::Defaults_operator`](#Sudo--Defaults_operator): custom datatype that validates sudo defaults operators

## Classes

### <a name="sudo"></a>`sudo`

This module manages sudo

#### Examples

##### 

```puppet
class { 'sudo': }
```

#### Parameters

The following parameters are available in the `sudo` class:

* [`enable`](#-sudo--enable)
* [`package`](#-sudo--package)
* [`package_manage`](#-sudo--package_manage)
* [`package_ldap`](#-sudo--package_ldap)
* [`package_ensure`](#-sudo--package_ensure)
* [`package_source`](#-sudo--package_source)
* [`package_provider`](#-sudo--package_provider)
* [`package_admin_file`](#-sudo--package_admin_file)
* [`purge`](#-sudo--purge)
* [`purge_ignore`](#-sudo--purge_ignore)
* [`suffix`](#-sudo--suffix)
* [`prefix`](#-sudo--prefix)
* [`config_file`](#-sudo--config_file)
* [`config_file_replace`](#-sudo--config_file_replace)
* [`config_file_mode`](#-sudo--config_file_mode)
* [`config_dir`](#-sudo--config_dir)
* [`config_dir_mode`](#-sudo--config_dir_mode)
* [`extra_include_dirs`](#-sudo--extra_include_dirs)
* [`content`](#-sudo--content)
* [`content_template`](#-sudo--content_template)
* [`content_string`](#-sudo--content_string)
* [`secure_path`](#-sudo--secure_path)
* [`ldap_enable`](#-sudo--ldap_enable)
* [`delete_on_error`](#-sudo--delete_on_error)
* [`validate_single`](#-sudo--validate_single)
* [`config_dir_keepme`](#-sudo--config_dir_keepme)
* [`use_sudoreplay`](#-sudo--use_sudoreplay)
* [`wheel_config`](#-sudo--wheel_config)
* [`sudoreplay_discard`](#-sudo--sudoreplay_discard)
* [`configs`](#-sudo--configs)
* [`defaults`](#-sudo--defaults)

##### <a name="-sudo--enable"></a>`enable`

Data type: `Boolean`

Ensure if present or absent.

Default value: `true`

##### <a name="-sudo--package"></a>`package`

Data type: `Optional[String[1]]`

Name of the package.
Only set this, if your platform is not supported or you know,
what you're doing.

Default value: `$sudo::params::package`

##### <a name="-sudo--package_manage"></a>`package_manage`

Data type: `Boolean`

Whether or not to manage the sudo package.

Default value: `true`

##### <a name="-sudo--package_ldap"></a>`package_ldap`

Data type: `Optional[String[1]]`

Name of the package with ldap support, if ldap_enable is set.

Default value: `$sudo::params::package_ldap`

##### <a name="-sudo--package_ensure"></a>`package_ensure`

Data type: `String[1]`

Allows you to ensure a particular version of a package

Default value: `$sudo::params::package_ensure`

##### <a name="-sudo--package_source"></a>`package_source`

Data type: `Optional[String[1]]`

Where to find the package. Only set this on AIX (required) and
Solaris (required), if your platform is not supported or you
know, what you're doing.

Default value: `$sudo::params::package_source`

##### <a name="-sudo--package_provider"></a>`package_provider`

Data type: `Optional[String[1]]`

Allows you to set a package provider.

Default value: `$sudo::params::package_provider`

##### <a name="-sudo--package_admin_file"></a>`package_admin_file`

Data type: `Optional[String[1]]`

Where to find a Solaris 10 package admin file for
an unattended installation. We do not supply a default file, so
this has to be staged separately and is required on Solaris 10.

Default value: `$sudo::params::package_admin_file`

##### <a name="-sudo--purge"></a>`purge`

Data type: `Boolean`

Whether or not to purge sudoers.d directory

Default value: `true`

##### <a name="-sudo--purge_ignore"></a>`purge_ignore`

Data type: `Optional[Variant[String[1], Array[String[1]]]]`

Files to exclude from purging in sudoers.d directory

Default value: `undef`

##### <a name="-sudo--suffix"></a>`suffix`

Data type: `Optional[String[1]]`

Adds a custom suffix to all files created in sudoers.d directory.

Default value: `undef`

##### <a name="-sudo--prefix"></a>`prefix`

Data type: `Optional[Pattern[/^[^.]+$/]]`

Adds a custom prefix to all files created in sudoers.d directory.

Default value: `undef`

##### <a name="-sudo--config_file"></a>`config_file`

Data type: `String[1]`

Main configuration file.
Only set this, if your platform is not supported or you know,
what you're doing.

Default value: `$sudo::params::config_file`

##### <a name="-sudo--config_file_replace"></a>`config_file_replace`

Data type: `Boolean`

Wether or not the config file should be replaced.

Default value: `true`

##### <a name="-sudo--config_file_mode"></a>`config_file_mode`

Data type: `String[1]`

The mode to set on the config file.

Default value: `$sudo::params::config_file_mode`

##### <a name="-sudo--config_dir"></a>`config_dir`

Data type: `String[1]`

Main directory containing sudo snippets, imported via
includedir stanza in sudoers file

Default value: `$sudo::params::config_dir`

##### <a name="-sudo--config_dir_mode"></a>`config_dir_mode`

Data type: `String[1]`

The mode to set for the config directory.

Default value: `$sudo::params::config_dir_mode`

##### <a name="-sudo--extra_include_dirs"></a>`extra_include_dirs`

Data type: `Optional[Array[String[1]]]`

Array of additional directories containing sudo snippets

Default value: `undef`

##### <a name="-sudo--content"></a>`content`

Data type: `Optional[String[1]]`

Alternate content template file location
*Deprecated*, use *content_template* instead.

Default value: `undef`

##### <a name="-sudo--content_template"></a>`content_template`

Data type: `Optional[String[1]]`

Alternate content template file location
Only set this, if your platform is not supported or you know,
what you're doing.
Note: some parameters won't work, if default template isn't
used

Default value: `undef`

##### <a name="-sudo--content_string"></a>`content_string`

Data type: `Optional[String[1]]`

Alternate config file content string
Note: some parameters won't work, if default template isn't
used

Default value: `undef`

##### <a name="-sudo--secure_path"></a>`secure_path`

Data type: `Optional[String[1]]`

The secure_path variable in sudoers.

Default value: `$sudo::params::secure_path`

##### <a name="-sudo--ldap_enable"></a>`ldap_enable`

Data type: `Boolean`

Enable ldap support on the package

Default value: `false`

##### <a name="-sudo--delete_on_error"></a>`delete_on_error`

Data type: `Boolean`

True if you want that the configuration is deleted on an error
during a complete visudo -c run. If false it will just return
an error and will add a comment to the sudoers configuration so
that the resource will be checked at the following run.

Default value: `true`

##### <a name="-sudo--validate_single"></a>`validate_single`

Data type: `Boolean`

Do a validate on the "single" file in the sudoers.d directory.
If the validate fail the file will not be saved or changed
if a file already exist.

Default value: `false`

##### <a name="-sudo--config_dir_keepme"></a>`config_dir_keepme`

Data type: `Boolean`

Add a .keep-me file to the config dir

Default value: `$sudo::params::config_dir_keepme`

##### <a name="-sudo--use_sudoreplay"></a>`use_sudoreplay`

Data type: `Boolean`

Boolean to enable the usage of sudoreplay.

Default value: `false`

##### <a name="-sudo--wheel_config"></a>`wheel_config`

Data type: `Enum['absent','password','nopassword']`

How to configure the wheel group in /etc/sudoers
Options are either not to configure it it, configure it prompting for password,
or configuring it without password prompt.

Default value: `$sudo::params::wheel_config`

##### <a name="-sudo--sudoreplay_discard"></a>`sudoreplay_discard`

Data type: `Optional[Array[String[1]]]`

Array of additional command to discard in sudo log.

Default value: `undef`

##### <a name="-sudo--configs"></a>`configs`

Data type: `Hash`

A hash of sudo::conf's

Default value: `{}`

##### <a name="-sudo--defaults"></a>`defaults`

Data type: `Sudo::Defaults`



Default value: `$sudo::params::defaults`

### <a name="sudo--allow"></a>`sudo::allow`

This class allows you to take complete advantage of automatic parameter
lookup using a Hiera database. Providing a singleton class that accepts
arrays in the parameters makes it possible to implement specific user
or group configuration in Hiera, whereas the use of defined types is
normally restricted to Puppet manifests.

Furthermore, having separate parameters for "add" and "replace" modes
allows you to take full advantage of inheritance in the Hiera database
while still allowing for exceptions if required.

#### Examples

##### 

```puppet
class { 'sudo::allow':
  add_users  => ['jsmith'],
  add_groups => ['wheel'],
}
```

#### Parameters

The following parameters are available in the `sudo::allow` class:

* [`add_users`](#-sudo--allow--add_users)
* [`add_groups`](#-sudo--allow--add_groups)
* [`replace_users`](#-sudo--allow--replace_users)
* [`replace_groups`](#-sudo--allow--replace_groups)

##### <a name="-sudo--allow--add_users"></a>`add_users`

Data type: `Array`

Define the set of users with sudo privileges by getting all values in
the hierarchy for this key, then flattening them into a single array
of unique values.

Default value: `[]`

##### <a name="-sudo--allow--add_groups"></a>`add_groups`

Data type: `Array`

Define the set of groups with sudo privileges by getting all values in
the hierarchy for this key, then flattening them into a single array
of unique values.

Default value: `[]`

##### <a name="-sudo--allow--replace_users"></a>`replace_users`

Data type: `Optional[Array]`

Override any values specified in add_users. If you specify this value
in your manifest or Hiera database, the contents of "add_users" will
be ignored. With Hiera, a standard priority lookup is used. Note that
if replace_users is specified at ANY level of the hierarchy, then
add_users is ignored at EVERY level of the hierarchy.

Default value: `undef`

##### <a name="-sudo--allow--replace_groups"></a>`replace_groups`

Data type: `Optional[Array]`

Override any values specified in add_groups. If you specify this value
in your manifest or Hiera database, the contents of "add_groups" will
be ignored. With Hiera, a standard priority lookup is used. Note that
if replace_groups is specified at ANY level of the hierarchy, then
add_groups is ignored at EVERY level of the hierarchy.

Default value: `undef`

## Defined types

### <a name="sudo--conf"></a>`sudo::conf`

Define: sudo::conf

#### Examples

##### 

```puppet
sudo::conf { 'admins':
  source => 'puppet:///files/etc/sudoers.d/admins',
}
```

#### Parameters

The following parameters are available in the `sudo::conf` defined type:

* [`ensure`](#-sudo--conf--ensure)
* [`priority`](#-sudo--conf--priority)
* [`content`](#-sudo--conf--content)
* [`source`](#-sudo--conf--source)
* [`template`](#-sudo--conf--template)
* [`sudo_config_dir`](#-sudo--conf--sudo_config_dir)
* [`sudo_file_name`](#-sudo--conf--sudo_file_name)
* [`sudo_syntax_path`](#-sudo--conf--sudo_syntax_path)

##### <a name="-sudo--conf--ensure"></a>`ensure`

Data type: `Enum['present', 'absent']`

Ensure if present or absent

Default value: `present`

##### <a name="-sudo--conf--priority"></a>`priority`

Data type: `Variant[String[1], Integer[0]]`

Prefix file name with $priority

Default value: `10`

##### <a name="-sudo--conf--content"></a>`content`

Data type: `Optional[Variant[Array[String[1]], String[1]]]`

Content of configuration snippet

Default value: `undef`

##### <a name="-sudo--conf--source"></a>`source`

Data type: `Optional[String[1]]`

Source of configuration snippet

Default value: `undef`

##### <a name="-sudo--conf--template"></a>`template`

Data type: `Optional[String[1]]`

Path of a template file

Default value: `undef`

##### <a name="-sudo--conf--sudo_config_dir"></a>`sudo_config_dir`

Data type: `Optional[String[1]]`

Where to place configuration snippets.
Only set this, if your platform is not supported or
you know, what you're doing.

Default value: `undef`

##### <a name="-sudo--conf--sudo_file_name"></a>`sudo_file_name`

Data type: `Optional[String[1]]`

Set a custom file name for the snippet

Default value: `undef`

##### <a name="-sudo--conf--sudo_syntax_path"></a>`sudo_syntax_path`

Data type: `String[1]`

Path to use for executing the sudo syntax check

Default value: `'/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin'`

## Functions

### <a name="sudo--defaults"></a>`sudo::defaults`

Type: Ruby 4.x API

Formats sudoers defaults config see https://linux.die.net/man/5/sudoers

    Default_Type ::= 'Defaults' |
                     'Defaults' '@' Host_List |
                     'Defaults' ':' User_List |
                     'Defaults' '!' Cmnd_List |
                     'Defaults' '>' Runas_List

    Default_Entry ::= Default_Type Parameter_List

    Parameter_List ::= Parameter |
                       Parameter ',' Parameter_List

    Parameter ::= Parameter '=' Value |
                  Parameter '+=' Value |
                  Parameter '-=' Value |
                  '!'* Parameter

The function is passed an Array of Tuples
e.g. [["env_reset", nil]]
     [["mailto", {"value" => root}]]

#### `sudo::defaults(Any *$args)`

Formats sudoers defaults config see https://linux.die.net/man/5/sudoers

    Default_Type ::= 'Defaults' |
                     'Defaults' '@' Host_List |
                     'Defaults' ':' User_List |
                     'Defaults' '!' Cmnd_List |
                     'Defaults' '>' Runas_List

    Default_Entry ::= Default_Type Parameter_List

    Parameter_List ::= Parameter |
                       Parameter ',' Parameter_List

    Parameter ::= Parameter '=' Value |
                  Parameter '+=' Value |
                  Parameter '-=' Value |
                  '!'* Parameter

The function is passed an Array of Tuples
e.g. [["env_reset", nil]]
     [["mailto", {"value" => root}]]

Returns: `String`

##### `*args`

Data type: `Any`



## Data types

### <a name="Sudo--Defaults"></a>`Sudo::Defaults`

sudo defaults

Alias of

```puppet
Hash[String, Variant[Struct[{
                                      Optional[list] => String,
                                      Optional[operator] => Sudo::Defaults_operator,
                                      Optional[value] => Variant[String,Numeric],
                                  }], Undef]]
```

### <a name="Sudo--Defaults_operator"></a>`Sudo::Defaults_operator`

custom datatype that validates sudo defaults operators

Alias of `Enum['=', '+=', '-=', '!']`

