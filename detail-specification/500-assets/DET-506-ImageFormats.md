##![Assets](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/assets.png)DET-505 Image Formats

# Image Formats Concept

The image formats for each is configured in an own config.  
The themes are in src/Client/WebsiteBundle/Resources/themes.  
Every theme has his own config under theme_name/config called image_formats.xml.


A XML could be look like this:

``` xml
<?xml version="1.0" ?>
<formats xmlns="http://schemas.sulu.io/media/formats"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://schemas.sulu.io/media/formats http://schemas.sulu.io/media/formats-1.0.xsd">
    <format>
        <name>50x50</name>
        <commands>
            <command>
                <action>scale</action>
                <parameters x="50" y="50" />
            </command>
        </commands>
    </format>
</formats>
```

## Format Reader

In the MediaBundle a service reads all formats from the themes and the internal Sulu formats.  
The service outputs the data in this format:

``` php
array(
    array( // one format
        'name' => '50x50', // name of the format
        'commands' => array( // commands to execute
            array(
                'action' => 'scale', // command name
                'parameters' => array( // command parameter
                    'x' => '50',
                    'y' => '50',
                )
            )
        )
    )
)
```

## Sulu formats

Sulu itself have three formats:  
 - 50x50 - Preview in Collection
 - 150x100 - Preview for Collection)
 - 170x170 - Content Type

This formats are configured in the SuluMediaBundle.  


## Handling Conflicts

If two themes have the same format, the commands and parameters from the first read will be used.  
So its important the name of the format reflect what the image converter does.