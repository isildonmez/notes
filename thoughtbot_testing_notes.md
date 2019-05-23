> From Upcase videos [factory_bot](https://thoughtbot.com/upcase/videos/factory-bot?utm_source=github&utm_medium=open-source&utm_campaign=factory-girl)

#### Why factory_bot?

Fixtures were tedious to write and led to testing antipatterns. factory_bot is intended to be a replacement for fixtures that makes it easier to produce test data while avoiding these antipatterns.

#### What are fixtures; why to move away from it?

- Fixtures are static data stored in a YAML file; you have to handwrite however many variants of objects that your tests will need, which can be tedious.

- It moves some of the complexity of a test out of the test itself, and makes it harder to understand at a glance.

- Fixtures are often all-or-nothing: If you have written several slightly different objects in your fixtures to support a few different tests, you have to load them all up every time; but not every test needs all of the objects.

#### FactoryBot vs fixtures

Factory_bot allows you to generate valid one-off objects as needed and you can dynamically send in data to override default attributes and create the variants that you need on a test-specific basis.

It tries to strike the right balance between conciseness and explicitness.
