- Feature Name: point_releases_on_a_schedule
- Start Date: 2020-02-15
- RFC PR: [rust-lang/rfcs#0000](https://github.com/rust-lang/rfcs/pull/0000)
- Rust Issue: [rust-lang/rust#0000](https://github.com/rust-lang/rust/issues/0000)

# Summary
[summary]: #summary

Currently, Rust's release schedule for stable point releases is ad-hoc, and
those wanting to backport changes into stable lack insight into this process.
This RFC proposes to ship a point release in the middle of our 6 week release
cycles. This means that we would expect a .1 release 3 weeks into the cycle.

# Motivation
[motivation]: #motivation

Over the past few months, the amount of pull requests nominated for stable
backport has hovered around ~8 per release cycle (XXX: can we collect some data
here?).

For each of these releases, that has meant that the bugs that these pull
requests fix have waited for 2-4 weeks to get into the hands of stable-only
users (they are usually nominated for beta backport as well). While this wait
time is not very long, it does increase the likelihood of new users seeing an
ICE in the compiler or otherwise having a subpar experience.

This RFC aims to ensure that small bugfixes to stable regressions wait at most 3
weeks before getting into the hands of users.

# Guide-level explanation
[guide-level-explanation]: #guide-level-explanation

Pull requests which may warrant backport to stable will be nominated by some
team member (usually, their author) during the first three weeks. After this
point, we're too close to the stable release for it to be worth issuing another
point release.

Pull requests approved by the compiler team for stable backport will be packaged
up into a stable-targeting PR and release notes written in preparation for the
point release early in the next week. Artifacts will be ready for testing on
dev-static.rust-lang.org by Monday night, with the release happening on Tuesday
in the 4th week.

The specific criteria for approval are left up to the compiler team (and
explicitly not defined in this RFC). However, this RFC does require that no
major changes land in a point release through this process.

Notably, point releases approved through this process should not get a dedicated
blog.rust-lang.org article; they are intended to be explicitly low-key to avoid
noise for the community.

 * Stable release on Thursday
 * Week 1
 * Week 2
 * Week 3: all stable backport nominations must be approved during compiler team meeting
 * Week 4:
    * artifacts ready by Monday night (usually prepared over the weekend)
    * stable point release on Tuesday
 * Week 5
 * Stable release on Thursday

# Drawbacks
[drawbacks]: #drawbacks

The primary drawback to this proposal is that it will increase churn for users
of Rust. Our release schedule, at every 6 weeks, is already one of the most
rapid in the compiler world; with this change, we would be issuing a release
roughly every 3 weeks. However, users are of course not required to migrate to
the stable point release, and the low-key nature of the midpoint point release
suggested by this RFC should help to alleviate this drawback.

# Rationale and alternatives
[rationale-and-alternatives]: #rationale-and-alternatives

We could be even more eager to issue point releases, for example following the
same policy as with beta: any PR accepted for beta-backport by the compiler team
will generally be rolled up and a beta release issued within 1-2 weeks of being
approved. This means that we usually have approximately 6 beta releases per
cycle. Presumably, we would have roughly 3 point releases with a similar policy
for stable backports. This is deemed too many.

We could also stay with the status quo, essentially only conducting a point
release if a relatively major bug is going to be fixed.

# Prior art
[prior-art]: #prior-art

TODO: Survey of point release policies in other projects.

# Unresolved questions
[unresolved-questions]: #unresolved-questions

- Should the release team sign off on these regularly scheduled point releases?

# Future possibilities
[future-possibilities]: #future-possibilities

No current future possibilities are known.
