DI Injection and Testing

#HSLIDE

Dependency injection is a design pattern that encourages writing decoupled code by passing components and services into a class.

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

Code example without DI

#HSLIDE

There are some problems here

#VSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

ContactController and ContactDAO are coupled

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

ContactController and ContactDAO are coupled

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

ContactDAO has a hard dependency on a specific database library

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

- Username and password get passed through multiple methods
- Need to copy the same db setup code if I want a OrganizationDAO

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

How do we test this? We have to have a test db set up, and we have to test the entire endpoint together
