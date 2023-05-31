# bower

## .bowerrc file

Bower can be configured using JSON syntax using .bowerrc files ( they can be more than one ).

<code>
{
  "directory": "app/components/",
  "timeout": 120000,
  "registry": {
    "search": [
      "http://localhost:8000",
      "https://bower.herokuapp.com"
    ]
  }
}
</code>

One of the most useful configuration variable is the **directory** parameter, that enable installation of modules in a custom path, other than //bower_component//.

A detailed description of available configuration variables can be found in [[https://github.com/bower/spec/blob/master/config.md|bower/spec]] repository.