DI Injection and Testing

#HSLIDE

Dependency injection is a design pattern that encourages writing decoupled code by passing components and services into a class.

#HSLIDE?gist=eb698ecf38712f53cb04ab54308e08b6

Code example without DI

#HSLIDE

What are the problems:
 - ContactController and ContactDAO are coupled - you can't use ContactController by itself
 - How do we test this? We have to have a test db set up, and we have to test the entire endpoint together
 - username and password get passed through multiple methods
 - ContactDAO has a hard dependency on a specific database library
 - Have to copy the same db setup code if I want a OrganizationDAO
