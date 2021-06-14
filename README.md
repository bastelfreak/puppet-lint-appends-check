puppet-lint-appends-check
====================================

[![License](https://img.shields.io/github/license/voxpupuli/puppet-lint-appends-check.svg)](https://github.com/voxpupuli/puppet-lint-appends-check/blob/master/LICENSE)
[![Test](https://github.com/voxpupuli/puppet-lint-appends-check/actions/workflows/test.yml/badge.svg)](https://github.com/voxpupuli/puppet-lint-appends-check/actions/workflows/test.yml)
[![Release](https://github.com/voxpupuli/puppet-lint-appends-check/actions/workflows/release.yml/badge.svg)](https://github.com/voxpupuli/puppet-lint-appends-check/actions/workflows/release.ym
l)
[![RubyGem Version](https://img.shields.io/gem/v/puppet-lint-appends-check.svg)](https://rubygems.org/gems/puppet-lint-appends-check)
[![RubyGem Downloads](https://img.shields.io/gem/dt/puppet-lint-appends-check.svg)](https://rubygems.org/gems/puppet-lint-appends-check)
[![Donated by Puppet Inc](https://img.shields.io/badge/donated%20by-Puppet%20Inc-fb7047.svg)](#transfer-notice)
A puppet-lint plugin to check that the append (+=) operator is unused.

## Installing

### From the command line

```shell
$ gem install puppet-lint-appends-check
```

### In a Gemfile

```ruby
gem 'puppet-lint-appends-check', :require => false
```

## Checks

### Append operator use

Use of the append operator can lead to unexpected behavior.

#### What you have done

```puppet
$ssh_users = ['myself', 'someone']

class test {
  $ssh_users += ['someone_else']
}
```

#### What you should have done

```puppet
$ssh_users = ['myself', 'someone', 'someone_else']

# OR
$ssh_users = hiera('ssh_users')
```

#### Auto fixing

There is not one way to properly fix this type of style error, so
running puppet-lint's fix feature will not have any effect.

#### Disabling the check

To disable this check, you can add `--no-appends-check` to your puppet-lint command line.

```shell
$ puppet-lint --no-appends-check path/to/file.pp
```

Alternatively, if you’re calling puppet-lint via the Rake task, you should insert the following line to your `Rakefile`.

```ruby
PuppetLint.configuration.send('disable_appends')
```
## Transfer Notice

This plugin was originally authored by [Puppet Inc](http://puppet.com).
The maintainer preferred that Puppet Community take ownership of the module for future improvement and maintenance.
Existing pull requests and issues were transferred over, please fork and continue to contribute here instead of Puppet Inc.

## License

This gem is licensed under the Apache-2 license.

## Release information

To make a new release, please do:
* update the version in the gemspec file
* Install gems with `bundle install --with release --path .vendor`
* generate the changelog with `bundle exec rake changelog`
* Check if the new version matches the closed issues/PRs in the changelog
* Create a PR with it
* After it got merged, push a tag. GitHub actions will do the actual release to rubygems and GitHub Packages
