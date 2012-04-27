Validator Component
===================

This component is based on the JSR-303 Bean Validation specification and
enables specifying validation rules for classes using XML, YAML or
annotations, which can then be checked against instances of these classes.

    use Symfony\Component\Validator\Validator;
    use Symfony\Component\Validator\Mapping\ClassMetadataFactory;
    use Symfony\Component\Validator\Mapping\Loader\StaticMethodLoader;
    use Symfony\Component\Validator\ConstraintValidatorFactory;

    $validator = new Validator(
        new ClassMetadataFactory(new StaticMethodLoader()),
        new ConstraintValidatorFactory()
    );

    $constraint = new Assert\Collection(array(
        'name' => new Assert\Collection(array(
            'first_name' => new Assert\MinLength(101),
            'last_name'  => new Assert\MinLength(1),
        )),
        'email' => new Assert\Email(),
        'simple' => new Assert\MinLength(102),
        'gender' => new Assert\Choice(array(3, 4)),
        'file' => new Assert\File(),
        'password' => new Assert\MinLength(60),
    ));

    $violations = $validator->validateValue($input, $constraint);

Resources
---------

Silex integration:

https://github.com/fabpot/Silex/blob/master/src/Silex/Provider/ValidatorServiceProvider.php

Documentation:

http://symfony.com/doc/2.0/book/validation.html

JSR-303 Specification:

http://jcp.org/en/jsr/detail?id=303

You can run the unit tests with the following command:

    phpunit

If you also want to run the unit tests that depend on other Symfony
Components, install dev dependencies before running PHPUnit:

    php composer.phar install --dev
