=======
CHANGES
=======

4.0.1 (unreleased)
------------------

- TBD

4.0.0 (2013-07-09)
------------------

- Updated ``boostrap.py`` to version 2.2.

- Bugfix: ZOPE_WATCH_CHECKERS=2 used to incorrectly suppress
  unauthorized/forbidden warnings.

- Bugfix: ZOPE_WATCH_CHECKERS=1 used to miss most of the checks.


4.0.0b1 (2013-03-11)
--------------------

- Added support for PyPy.

- Fixed extension compilation on windows python 3.x


4.0.0a5 (2013-02-28)
--------------------

- Undo changes from 4.0.0a4. Instead, ``zope.untrustedpython`` is only
  included during Python 2 installs.


4.0.0a4 (2013-02-28)
--------------------

- Remove ``untrustedpython`` extra again, since we do not want to support
  ``zope.untrustedpython`` in ZTK 2.0. If BBB is really needed, we will create
  a 3.10.0 release.

4.0.0a3 (2013-02-15)
--------------------

- Fix test breakage in 4.0.0a2 due to deprecation strategy.

4.0.0a2 (2013-02-15)
--------------------

- Added back the ``untrustedpython`` extra:  now pulls in
  ``zope.untrustedpython``.  Restored deprecated backward-compatible imports
  for ``zope.security.untrustedpython.{builtins,interpreter,rcompile}``
  (the extra and the imports are to be removed in version 4.1).


4.0.0a1 (2013-02-14)
--------------------

- Added support for Python 3.2 and 3.3.

- 100% unit test coverage.

- ``zope.security.untrustedpython`` moved to separate project:
  ``zope.untrustedpython``

- Converted use of ``assert`` in non-test code to apprpriate error types:

  - Non-dict's passed to ``Checker.__init__``.

- Removed dprecattion of ``zope.security.adapter.TrustedAdapterFactory``.
  Although it has been marked as deprectaed since before Zope3 3.2, current
  versions of ``zope.compoent`` still rely on it.

- Converted doctests to Sphinx documentation in 'docs'.

- Added 'setup.py docs' alias (installs ``Sphinx`` and dependencies).

- Added 'setup.py dev' alias (runs ``setup.py develop`` plus installs
  ``nose`` and ``coverage``).

- Made non-doctest tests fully independent of ``zope.testing``.

  Two modules, ``zope.security.checker`` and ``zope.security.management``,
  register cleanups with ``zope.testing`` IFF it is importable, but the
  tests no longer rely on it.

- Enabled building extensions without the 'svn:external' of the ``zope.proxy``
  headers into our 'include' dir.

- Bumped ``zope.proxy`` dependency to ">= 4.1.0" to enable compilation
  on Py3k.

- Replaced deprecated ``zope.component.adapts`` usage with equivalent
  ``zope.component.adapter`` decorator.

- Replaced deprecated ``zope.interface.classProvides`` usage with equivalent
  ``zope.interface.provider`` decorator.

- Replaced deprecated ``zope.interface.implements`` usage with equivalent
  ``zope.interface.implementer`` decorator.

- Dropped support for Python 2.4 and 2.5.

- Added test convenience helper ``create_interaction`` and
  ``with interaction()``.

3.9.0 (2012-12-21)
------------------

- Pin ``zope.proxy >= 4.1.0``

- Ship with an included ``proxy.h`` header which is compatible with the
  4.1.x version ov ``zope.proxy``.

3.8.5 (2012-12-21)
------------------

- Ship with an included ``proxy.h`` header which is compatible with the
  supported versions of ``zope.proxy``.

3.8.4 (2012-12-20)
------------------

- Pin ``zope.proxy >= 3.4.2, <4.1dev``

3.8.3 (2011-09-24)
------------------

- Fixed a regression introduced in 3.8.1: ``zope.location``\'s LocationProxy
  did not get a security checker if ``zope.security.decorator`` was not
  imported manually. Now ``zope.security.decorator`` is imported in
  ``zope.security.proxy`` without re-introducing the circular import fixed in
  3.8.1.

3.8.2 (2011-05-24)
------------------

- Fix a test that failed on Python 2.7.


3.8.1 (2011-05-03)
------------------

- Fixed circular import beween ``zope.security.decorator`` and
  ``zope.security.proxy`` which led to an ``ImportError`` when only
  importing ``zope.security.decorator``.


3.8.0 (2010-12-14)
------------------

- Added tests for our own ``configure.zcml``.

- Added ``zcml`` extra dependencies, run related tests only if
  ``zope.configuration`` is available.

- Run tests related to the ``untrustedpython`` functionality only if
  ``RestrictedPython`` is available.


3.7.3 (2010-04-30)
------------------

- Prefer the standard libraries doctest module to the one from zope.testing.

- Fixed directlyProvides IVocabularyFactory for PermissionIdsVocabulary in
  Python code, even if it's unnecessary because IVocabularyFactory is provided
  in zcml.

- Removed the dependency on the zope.exceptions package: zope.security.checker
  now imports ``DuplicationError`` from zope.exceptions if available, otherwise
  it defines a package-specific ``DuplicationError`` class which inherits from
  Exception.


3.7.2 (2009-11-10)
------------------

- Added compatibility with Python 2.6 abstract base classes.


3.7.1 (2009-08-13)
------------------

- Fix for LP bug 181833 (from Gustavo Niemeyer). Before "visiting" a
  sub-object, a check should be made to ensure the object is still valid.
  Because garbage collection may involve loops, if you garbage collect an
  object, it is possible that the actions done on this object may modify the
  state of other objects. This may cause another round of garbage collection,
  eventually generating a segfault (see LP bug). The Py_VISIT macro does the
  necessary checks, so it is used instead of the previous code.


3.7.0 (2009-05-13)
------------------

- Made ``pytz`` a soft dependency:  the checker for ``pytz.UTC`` is
  created / tested only if the package is already present.  Run
  ``bin/test_pytz`` to run the tests with ``pytz`` on the path.


3.6.3 (2009-03-23)
------------------

- Ensure that simple zope.schema's VocabularyRegistry is used for
  PermissionVocabulary tests, because it's replaced implicitly in
  environments with zope.app.schema installed that makes that tests
  fail.

- Fixed a bug in DecoratedSecurityCheckerDescriptor which made
  security-wrapping location proxied exception instances throw
  exceptions on Python 2.5.
  See https://bugs.launchpad.net/zope3/+bug/251848


3.6.2 (2009-03-14)
------------------

- Add zope.i18nmessageid.Message to non-proxied basic types. It's okay, because
  messages are immutable. It was done by zope.app.security before.

- Add "__name__" and "__parent__" attributes to list of available by default.
  This was also done by zope.app.security package before.

- Added PermissionsVocabulary and PermissionIdsVocabulary vocabularies
  to the ``zope.security.permission`` module. They were moved from
  the ``zope.app.security`` package.

- Add zcml permission definitions for most common and useful permissions,
  like "zope.View" and "zope.ManageContent", as well as for the special
  "zope.Public" permission. They are placed in a separate "permissions.zcml"
  file, so it can be easily excluded/redefined. They are selected part of
  permissions moved from ``zope.app.security`` and used by many zope.*
  packages.

- Add `addCheckerPublic` helper function in ``zope.security.testing`` module
  that registers the "zope.Public" permission as an IPermission utility.

- Add security declarations for the ``zope.security.permisson.Permission``
  class.

- Improve test coverage.


3.6.1 (2009-03-10)
------------------

- Use ``from`` imports instead of ``zope.deferred`` to avoid circular
  import problems, thus drop dependency on ``zope.deferredimport``.

- Raise NoInteraction when zope.security.checkPermission is called
  without interaction being active (LP #301565).

- Don't define security checkers for deprecated set types from the
  "sets" module on Python 2.6. It's discouraged to use them and
  `set` and `frozenset` built-in types should be used instead.

- Change package's mailng list address to zope-dev at zope.org as
  zope3-dev at zope.org is now retired.

- Remove old zpkg-related files.


3.6.0 (2009-01-31)
------------------

- Install decorated security checker support on LocationProxy from the
  outside.

- Added support to bootstrap on Jython.

- Moved the `protectclass` module from `zope.app.security` to this
  package to reduce the number of dependencies on `zope.app.security`.

- Moved the <module> directive implementation from `zope.app.security`
  to this package.

- Moved the <class> directive implementation from `zope.app.component`
  to this package.


3.5.2 (2008-07-27)
------------------

- Made C code compatible with Python 2.5 on 64bit architectures.


3.5.1 (2008-06-04)
------------------

- Add `frozenset`, `set`, `reversed`, and `sorted` to the list of safe
  builtins.


3.5.0 (2008-03-05)
------------------

- Changed title for ``zope.security.management.system_user`` to be more
  presentable.


3.4.3 - (2009/11/26)
--------------------

- Backported a fix made by Gary Poster to the 3.4 branch:
  Fix for LP bug 181833 (from Gustavo Niemeyer). Before "visiting" a
  sub-object, a check should be made to ensure the object is still valid.
  Because garbage collection may involve loops, if you garbage collect an
  object, it is possible that the actions done on this object may modify the
  state of other objects. This may cause another round of garbage collection,
  eventually generating a segfault (see LP bug). The Py_VISIT macro does the
  necessary checks, so it is used instead of the previous code.


3.4.2 - (2009/03/23)
--------------------

- Added dependency 'zope.thread' to setup.py, without the tests were
  failing.

- Backported a fix made by Albertas Agejevas to the 3.4 branch. He
  fixed a bug in DecoratedSecurityCheckerDescriptor which made
  security-wrapping location proxied exception instances throw
  exceptions on Python 2.5.  See
  https://bugs.launchpad.net/zope3/+bug/251848


3.4.1 - 2008/07/27
------------------

- Made C code compatible with Python 2.5 on 64bit architectures.


3.4.0 (2007-10-02)
------------------

- Updated meta-data.


3.4.0b5 (2007-08-15)
--------------------

- Bug: Fixed a circular import in the C implementation.


3.4.0b4 (2007-08-14)
--------------------

- Bug: ``zope.security.management.system_user`` had an ugly/brittle id.


3.4.0b3 (2007-08-14)
--------------------

- ``zope.security`` now works on Python 2.5

- Bug: ``zope.security.management.system_user`` wasn't a valid principal
  (didn't provide IPrincipal).

- Bug: Fixed inclusion of doctest to use the doctest module from
  ``zope.testing``. Now tests can be run multiple times without
  breaking. (#98250)


3.4.0b2 (2007-06-15)
--------------------

- Bug: Removed stack extraction in newInteraction. When using eggs this is an
  extremly expensive function. The publisher is now more than 10 times faster
  when using eggs and about twice as fast with a zope trunk checkout.


3.4.0b1
-------

- Temporarily fixed the hidden (and accidental) dependency on zope.testing to
  become optional.

Note: The releases between 3.2.0 and 3.4.0b1 where not tracked as an
individual package and have been documented in the Zope 3 changelog.


3.2.0 (2006-01-05)
------------------

- Corresponds to the verison of the zope.security package shipped as part of
  the Zope 3.2.0 release.

- Removed deprecated helper functions, 'proxy.trustedRemoveSecurityProxy' and
  'proxy.getProxiedObject'.

- Made handling of 'management.{end,restore}Interaction' more careful w.r.t.
  edge cases.

- Made behavior of 'canWrite' consistent with 'canAccess':  if 'canAccess'
  does not raise 'ForbiddenAttribute', then neither will 'canWrite'.  See:
  http://www.zope.org/Collectors/Zope3-dev/506

- Code style / documentation / test fixes.


3.1.0 (2005-10-03)
------------------

- Added support for use of the new Python 2.4 datatypes, 'set' and
  'frozenset', within checked code.

- C security proxy acquired a dependency on the 'proxy.h' header from the
  'zope.proxy' package.

- XXX: the spelling of the '#include' is bizarre!  It seems to be related to
  'zpkg'-based builds, and should likely be revisited.  For the moment, I have
  linked in the 'zope.proxy' package into our own 'include' directory.  See
  the subversion checkin: http://svn.zope.org/Zope3/?rev=37882&view=rev

- Updated checker to avoid re-proxying objects which have and explicit
  '__Security_checker__' assigned.

- Corresponds to the verison of the zope.security package shipped as part of
  the Zope 3.1.0 release.

- Clarified contract of 'IChecker' to indicate that its 'check*' methods may
  raise only 'Forbidden' or 'Unauthorized' exceptions.

- Added interfaces, ('IPrincipal', 'IGroupAwarePrincipal', 'IGroup', and
  'IPermission') specifying contracts of components in the security framework.

- Code style / documentation / test fixes.


3.0.0 (2004-11-07)
------------------

- Corresponds to the version of the zope.security package shipped as part of
  the Zope X3.0.0 release.
