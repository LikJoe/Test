<?php

/**
 * Created by JetBrains PhpStorm.
 * User: PCPC
 * Date: 13-4-21
 * Time: 下午9:44
 * To change this template use File | Settings | File Templates.
 */
class EventsController extends AppController {

    public $helpers = array('Js');
    public $components = array('RequestHandler');

    public function index() {
        $this->set("events", $this->Event->find("all", array('order' => 'event_category_name ASC')));
        //$this->set("event_categories",$this->EventCategory->find("all",array('order' => 'event_category_name ASC')));
    }

    public function add() {
        $this->loadModel('EventCategory');
        $event_categories = $this->EventCategory->find('list');
        $this->set(compact('event_categories'));
        if ($this->request->is('post')) {
            $this->Event->create();
            if ($this->Event->save($this->request->data)) {
                $this->Session->setFlash('The event has been saved');
                $this->redirect(array('action' => 'index'));
            } else {
                $this->Session->setFlash('The event could not be saved. Please try again.');
            }
        }
    }

    public function view($id = null) {
        $this->Event->id = $id;
        $this->set("event", $this->Event->findById($id));
    }

    public function edit($id = null) {
        $this->Event->id = $id;
        if (empty($this->data)) {
            $this->data = $this->Event->findById($id);
        } else {
            if ($this->Event->save($this->data)) {
                if ($this->request->is('ajax')) {
                    $this->render('success', 'ajax');
                } else {
                    $this->Session->setFlash('Event Updated Successfully');
                    $this->redirect(array('action' => 'index'));
                }
            }
        }
        $this->loadModel('EventCategory');
        $event_category = $this->EventCategory->find('list', array('fields' => array('event_category_name')));
        $this->set('event_categories', $event_category);
    }

    function delete($id) {
        $this->Session->setFlash('This event has been deleted.');
        $this->Event->delete($id);
        $this->redirect(array('action' => 'index'));
    }

    public function validate_form() {
        if ($this->request->is('ajax')) {
            $this->data['Event'][$this->params['form']['field']] = $this->params['form']['value'];
            $this->Event->set($this->data);
            if ($this->Event->validate()) {
                $this->autoRender = FALSE;
            } else {
                $error = $this->validateErrors($this->Event);
                $this->set('error', $error[$this->params['form']['field']]);
            }
        }
    }

}

