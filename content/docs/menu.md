---
view::extends: _includes.docs_post_base
view::yields: post_body
pageTitle: - Laravel Admin panel menu
---
@verbatim
# Admin Menu
----------

The panel menu is an element of the admin interface,
Allows you to select one of several listed software options.
It is an important element of the graphical user interface.

The menu in Orchid is divided into several areas, which in turn can be
Containers for another menu.



### Using:

To register a new menu for your package or module, you need to
Specify it in the composer provider.
	
```php
<?php

namespace App\Http\Composers;

use Orchid\Kernel\Dashboard;

class MenuComposer
{
    /**
     * MenuComposer constructor.
     *
     * @param Dashboard $dashboard
     */
    public function __construct(Dashboard $dashboard)
    {
        $this->dashboard = $dashboard;
    }

    public function compose()
    {
        $this->dashboard->menu->add('Main', [
            'slug'       => 'slug-my-menu',
            'icon'       => 'icon',
            'route'      => '#',
            'label'      => 'My name Menu',
            'childs'     => true,
            'main'       => true,
            'active'     => 'dashboard.mymenu.*',
            'permission' => 'dashboard.mymenu',
            'sort'       => 1,
        ]);
    }
}
```

 
 @endverbatim
