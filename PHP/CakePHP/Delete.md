```
/**
 * Delete method
 *
 * @param string|null $id Category id.
 * @return \Cake\Http\Response|null Redirects to index.
 * @throws \Cake\Datasource\Exception\RecordNotFoundException When record not found.
 */
public function delete($id = null){
    $this->request->allowMethod(['post', 'delete']);
    $category = $this->Categories->get($id);
    
    try {
        $this->Categories->delete($category);
        
        $this->Flash->success(__('The category has been deleted.'));
        return $this->redirect(['action' => 'index']);
    } catch (\PDOException $e) {
        // The exact error message is $e->getMessage();
        if($e->getCode() == '23503') {
            $this->Flash->error(__('The item you are trying to delete is associated with other records.'));
            return $this->redirect(['action' => 'index']);
        } else {
            $this->Flash->error(__('The category could not be deleted. Please, try again.'));
            $this->Flash->error($e->getMessage());
        }
    }
}
```