---
view::extends: _includes.docs_post_base
view::yields: post_body
pageTitle: - Types
---
@verbatim
#Types 
----------

Types are the main part of Orchid, instead of generating a CRUD for each model
You can select any entity in a separate type and easily operate it


Own types must be registered in `config/content.php` in the types section

The type looks like this:

```php
<?php

namespace Orchid\Foundation\Types;

use Orchid\Foundation\Http\Forms\Posts\BasePostForm;
use Orchid\Foundation\Http\Forms\Posts\UploadPostForm;
use Orchid\Type\Type;

class TestType extends Type
{
    /**
     * @var string
     */
    public $name = 'Тестовый тип';

    /**
     * @var string
     */
    public $slug = 'test';

    /**
     * Slug url /news/{name}.
     *
     * @var string
     */
    public $slugFields = 'name';

    /**
     * @var bool
     */
    public $api = true;

    /**
     * Rules Validation.
     *
     * @return array
     */
    public function rules()
    {
        return [
            'id'             => 'sometimes|integer|unique:posts',
            'content.*.name' => 'required|string',
            'content.*.body' => 'required|string',
        ];
    }

    /**
     * @return array
     */
    public function fields()
    {
        return [
            'name' => 'tag:input|type:text|name:name|max:255|required|title:Название статьи|help:Упоменение',
            'body' => 'tag:textarea|name:body|max:255|required|class:summernote|rows:10',
            'place'    => 'tag:place|type:text|name:place|max:255|required|title:Место положение|help:Адрес на карте',
            'datetime' => 'tag:datetime|type:text|name:open|max:255|required|title:Дата открытия|help:Открытие мероприятия состоиться',
            'title'       => 'tag:input|type:text|name:title|max:255|required|title:Заголовок статьи|help:Упоменение',
            'description' => 'tag:textarea|name:description|max:255|required|rows:5|title:Краткое описание',
            'keywords'    => 'tag:tags|name:keywords|max:255|required|title:Ключевые слова|help:Упоменение',
            'robot'       => 'tag:robot|name:robot|max:255|required|title:Индексация|help:Разрешить поисковым роботам индесацию страницы',
            'free' => 'tag:checkbox|name:robot|max:255|required|title:Бесплатно|help:Мероприятие бесплатно|placeholder:Мероприятие бесплатно|default:1',

        ];
    }

    /**
     * @return array
     */
    public function modules()
    {
        return [
            UploadPostForm::class,
            BasePostForm::class,
        ];
    }

    /**
     * Grid View for post type.
     */
    public function grid()
    {
        return [
            'name'       => 'Название',
            'publish'    => 'Дата публикации',
            'created_at' => 'Дата создания',
        ];
    }
}

```

Where:
1. $ name - type name
1. $ slug - a unique value that explicitly defines this type
1. $ slugName is responsible for generating the CNC in the field
1. rules () - validation rules
1. fields () - required fields
1. modules () - realizing forms
1. grid () - displaying the table

You can extend the data type with all the available methods to add a new functionality to it that corresponds to your application
 
@endverbatim