modalForm for Yii2
========================
Изменения
------------
Assets заменены на boostrap4

Добавлена поддержка доп. классов модального окна. [Подробнее о классах](https://getbootstrap.su/docs/4.6/components/modal/).

Установка
------------
Добавить в файл `composer.json`:
```
"repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/elisevgeniy/modal-form"
        }
    ]
    
"require": {
        "vsk/modal-form": "dev-bootstrap4"
    },
```
После добавления выполнить `composer require "vsk/modal-form"`


Usage
-----
![Edit modal example](./resources/images/modalForm.gif?raw=true)



Include in controller

```
class TestController extends Controller
{

    public function actions()
    {
        return [
            'modal-form' => [
                'class' => ModalFormAction::class,
                'getBody' => function ($action) {
                    return $this->render('@vendor/vsk/modal-form/src/test/views/modal-list');
                },
                'getTitle' => function() {
                    return 'Список тестовых данных';
                },
            ],
            'modal-form-update' => [
                'class' => ModalFormAction::class,
                'getBody' => function ($action) {
                    return $this->render('@vendor/vsk/modal-form/src/test/views/update', [
                        'model' => $action->getModel(),
                    ]);
                },
                'getTitle' => function() {
                    return 'title';
                },
                'getModel' => function () {
                    $id = \Yii::$app->request->get('id');
                    return Test::findOne($id);
                },
                'submitForm' => function ($action) {
                    $model = $action->getModel();
                    $model->load(\Yii::$app->request->post());
                    return $model->save();
                }
            ],
        ];
    }
}

```

Include in you view

```
<?php

echo \vsk\modalForm\ModalFormWidget::widget([
                     'additionalModalClasses' => 'modal-xl',
                     'template' => function ($widget) {
                         $id = $widget->getId();
                         return "<button id='{$id}' data-modal-url='/adminx24/test/modal-form'>TEST</button>";
                     }
                 ]);

```
