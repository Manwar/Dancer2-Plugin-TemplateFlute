# NAME

Dancer2::Plugin::TemplateFlute - Dancer2 form handler for Template::Flute template engine

# VERSION

Version 0.202

# SYNOPSIS

Display template with checkout form:

    get '/checkout' => sub {
        my $form;

        $form = form( name => 'checkout', source => 'session' );
        
        template 'checkout', { form => $form };
    };

Retrieve form input from checkout form body:

    post '/checkout' => sub {
        my ($form, $values);

        $form = form( name => 'checkout', source => 'body' );
        $values = $form->values;
    };

Reset form after completion to prevent old data from
showing up on new form:

    form('checkout')->reset;

If you have multiple forms then just pass the form token as an array reference:

    get '/cart' => sub {
        my ( $cart_form, $inquiry_form );

        # 'source' defaults to 'session' if not provided
        $cart_form    = form( name => 'cart' );

        # equivalent to form( name => 'inquiry' )
        $inquiry_form = form( 'inquiry' );
        
        template 'checkout', { form => [ $cart_form, $inquiry_form ] };
    };

# KEYWORDS

## form &lt;$name|%params>

The following `%params` are recognised:

### name

The name of the form. Defaults to 'main'.

### values

    my $form = form( 'main', values => $params );

The form parameters as a [Hash::MultiValue](https://metacpan.org/pod/Hash::MultiValue) object or something that can
be coerced into one.

Instead of ["values"](#values) you can also use ["source"](#source) to set initial values.

### source

    my $form = form( name => 'main', source => 'body' );

The following values are valid:

- body

    This sets the form values to the request body parameters
    [Dancer2::Core::Request::body\_parameters](https://metacpan.org/pod/Dancer2::Core::Request::body_parameters).

- query

    This sets the form values to the request query parameters
    [Dancer2::Core::Request::query\_parameters](https://metacpan.org/pod/Dancer2::Core::Request::query_parameters).

- parameters

    This sets the form values to the combined body and request query parameters
    [Dancer2::Core::Request::parameters](https://metacpan.org/pod/Dancer2::Core::Request::parameters).

- session

    Reads in values from the session. This is the default if no ["source"](#source) or
    ["parameters"](#parameters) are specified.

**NOTE:** if both ["source"](#source) and ["values"](#values) are supplied then [values](https://metacpan.org/pod/values) is
ignored.

See [Dancer2::Plugin::TemplateFlute::Form](https://metacpan.org/pod/Dancer2::Plugin::TemplateFlute::Form) for details of other parameters
that can be used.

# DESCRIPTION

`Dancer2::Plugin::TemplateFlute` is used for forms with the
[Dancer2::Template::TemplateFlute](https://metacpan.org/pod/Dancer2::Template::TemplateFlute) templating engine.    

Form fields, values and errors are stored into and loaded from the session key
`form`.

# AUTHORS

Original Dancer plugin by:

Stefan Hornburg (Racke), `<racke at linuxia.de>`

Initial port to Dancer2 by:

Evan Brown (evanernest), `evan at bottlenose-wine.com`

Rehacking to Dancer2's plugin2 and general rework:

Peter Mottram (SysPete), `peter at sysnix.com`

# BUGS

Please report any bugs or feature requests via GitHub issues:
[https://github.com/interchange/Dancer2-Plugin-TemplateFlute/issues](https://github.com/interchange/Dancer2-Plugin-TemplateFlute/issues).

We will be notified, and then you'll automatically be notified of progress
on your bug as we make changes.

# ACKNOWLEDGEMENTS

# LICENSE AND COPYRIGHT

Copyright 2011-2016 Stefan Hornburg (Racke).

Copyright 2015-1016 Evan Brown.

Copyright 2016 Peter Mottram (SysPete).

This program is free software; you can redistribute it and/or modify it
under the terms of either: the GNU General Public License as published
by the Free Software Foundation; or the Artistic License.

See http://dev.perl.org/licenses/ for more information.
