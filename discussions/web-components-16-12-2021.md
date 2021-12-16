# Web Components Kick Off

## Thursday 16th December, 2021

### Attendees

* Trygve
* Dave
* Benjamin
* Richard

### Notes

#### Thoughts on approach

Trygve summarised some thoughts about why it makes sense to use an abstraction such as Lit Element/HTML on top of the raw custom elements spec. 
This revolved mostly around smoothing over some of the funky edges of the raw spec, avoiding misusing the spec and also ensuring good performance.

#### Discussion around how builds are done

Discussion around whether it would make sense to change the way we do core builds at the moment to try to leverage the advantages of TW's purge system.
Trygve suggested we could:
* run our own purge on the TW we use in our components lib to produce a core components lib that is shared optimally via Eik across all apps.
* Allow apps to use TW purge directly in conjunction with our TW config file that produces an optimal build for the app with component classes removed.

#### Discussion around issue 24 and how that relates

Discussion around using Fabric in apps that don't currently use Frameworks such as the frontpage, and market frontpages. This stems from discussion on this issue: 
https://github.com/fabric-ds/issues/issues/24

Main contending options to solve are:
* use the component classes package
* use web components. 

However, it would also be possible to use Lit HTML to smooth this quite a bit. 
If we made it possible for apps to use component templates directly via Lit HTML we could support server side only apps.

#### The way forward

We think we should start to experiment around writing components with Lit Element/HTML. Good to have a project to work on along side building components
and the a rewrite of the frontpage might suffice for this. Perhaps early in the new year.

#### Action points

- [ ] Discuss with Frode to see if rewriting frontpage using WC/CE is an option
- [ ] Planning, break into tasks early in the new year
