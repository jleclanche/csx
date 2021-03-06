CSX - CSS Extended
~~~~~~~~~~~~~~~~~~

.. NOTE::
   CSX is a preliminary draft for a spec that predates `SCSS <http://sass-lang.com>`.
   It is only here for historical purposes.

**Variables**

Variables let you store any css value and reuse them in a property::

	$myGreen: #33dd33;
	body { color: $myGreen; }

Implemented by Sass as `variables <http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#variables_>`

**Classes**

Classes are an easy way to define a set of properties you want to reuse througout the file::

	$myClass {
		color: green;
		border-color: blue;
	}

**Inheritance**

Inheritance allows you to reuse the same set of properties defined in another class, selector, or even a set of classes and/or selectors.
Properties can be overridden by rewriting them in the subclass::

	.foo {
		@inherits($myClass);
		/* "Replaces" the inherit by the properties defined in $myclass */
		border-size: 1px;
	}

	$myOtherClass {
		padding-top: 10px;
	}

	.baz {
		@inherits(.foo, $myOtherClass);
		border-color: black;
	}

Implementation by Sass `extends <http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#extend>` existing css classes, and separately implements `mixins <http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#mixins>`.

**Property nesting**

Property nesting lets you inherit properties from a parent selector. This helps keep your css clearly organized and indented::

	div {
		.abc {
			/* div .abc */
		}
		#abc {
			/* div #abc */
		}
		$.abc {
			/* div.abc */
		}
	}

Sass supports `nested rules <http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#nested_rules>`.

**Operators**

Operators can be used to reuse variables such as sizes and work with them relatively. Trying to mix units will result in an error::

	$fontSize: 12px;
	h1 {
		font-size: $fontSize + 4px;
	}
	small {
		font-size: $fontSize - 2px;
	}
	$myCompany: "My Company";
	#welcome {
		content: "Welcome to " + $myCompany + "!";
	}

Sass supports a wide range of `operations <http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#operations>`.

**Color operations**

Operators work on colors as well, letting you darken and brighten them by a percentage or a hex number::

	$myGreen: #33dd33;
	.paleGreen {
		color: $myGreen + #222;
	}
	.darkGreen {
		color: $myGreen - 10%;
	}

Sass supports `color operations <http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#color_operations>`.

**Multi-property assignments**

With multi-property assignments, you avoid repetition when you want the same values for two different properties::

	.cls {
		border-top, border-bottom: 1px solid black;
	}

Unsupported by Sass.

**Builtin sprite support**

Sprites made easy. The sprite() function will return an image (or an error, accordingly) when passed an url, x/y coords and x/y dimensions.
The compiler will automagically transform this image into correct positions and sizes::

	$mySprite: url(/img/sprite.png);
	$logo: sprite($mySprite, 0, 0, 30, 20); /* Coords in the image */
	$logo2: sprite(url(/img/sprite2.png), 0, 0, 20, 20);

	.cls2 { background-image: $logo2; }
	.cls3 { background-image: sprite(url(/img/sprite3.png), 0, 0, 15, 25); }

Unsupported by Sass

**Compile-time file inclusion**

The preprocessor can include and parse external files directly::

	@include("misc.csx");

... or even include them in base64 (TBD)::

	$logo: @b64include("logo.png");
	.logo {
		background-image: url("data:image/png;base64," + $logo);
	}

Unsupported by Sass.
