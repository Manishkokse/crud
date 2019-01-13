<?php
class User_model extends CI_Model {
 
    public function __construct()
    {
        $this->load->database();
    }
    
    public function get_user($id = 0)
    {
        if ($id === 0)
        {
            $query = $this->db->get('users');
            return $query->result_array();
        }
 
        $query = $this->db->get_where('users', array('id' => $id));
        return $query->row_array();
    }
    
    public function get_user_login($email, $password)
    {
        $query = $this->db->get_where('users', array('email' => $email, 'password' => md5($password)));        
        //return $query->num_rows();
        return $query->row_array();
    }
    
    public function set_user($id = 0)
    {
$file_name='';
if(!empty($_FILES["picture"]["name"])){
					$target_dir = FULL_PATH."uploads/";
					$exp=explode('.',$_FILES["picture"]["name"]);
					$ext=end($exp);
					$file_name = time().mt_rand(5, 10).".".$ext;   
					$target_file = $target_dir . $file_name;
					$uploadOk = 1;
					$imageFileType = strtolower(pathinfo($target_file,PATHINFO_EXTENSION));
					 $check = getimagesize($_FILES["picture"]["tmp_name"]);
					
					    if($check !== false) {
						
						$uploadOk = 1;
					    } else {
						
						$uploadOk = 0;
					    }

					
					if (file_exists($target_file)) {
					   
					    $uploadOk = 0;
					}
					
					if ($_FILES["picture"]["size"] > 500000) {
						$this->session->set_flashdata('msg_error', 'Sorry, your file is too large.');
						 $uploadOk = 0;
						redirect('users/register');

					}
					
					if($imageFileType != "jpg" && $imageFileType != "png" && $imageFileType != "jpeg"
					&& $imageFileType != "gif" ) {
					$this->session->set_flashdata('msg_error', 'Sorry, only JPG, JPEG, PNG & GIF files are allowed');
						 $uploadOk = 0;
						redirect('users/register');    
					   
					}
					
					if ($uploadOk == 0) {
					    $this->session->set_flashdata('msg_error', 'Sorry, there was an error uploading your file');
						redirect('users/register');
					} else {
						//echo $target_file;exit;
					    if (move_uploaded_file($_FILES["picture"]["tmp_name"], $target_file)) {
						//echo "The file ". basename( $_FILES["fileToUpload"]["name"]). " has been uploaded.";
						$this->session->set_flashdata('msg_success', 'has been uploaded');
						//redirect('users/register');
					    } else {
						//echo "Sorry, there was an error uploading your file.";
						$this->session->set_flashdata('msg_error', 'Sorry, there was an error uploading your file');
						redirect('users/register');
					    }
					}
				}
        $data = array(
            'firstname' => $this->input->post('firstname'),
            'lastname' => $this->input->post('lastname'),
            'email' => $this->input->post('email'),
            'password' => $this->input->post('password'),
		'mobile' => $this->input->post('mobile'),
		'gender' => $this->input->post('gender'),
		'picture' => $file_name,
            'created' => date('Y-m-d H:i:s')
        );
            
        if ($id == 0) {
	//echo "fdfdsfdsf";exit;
            return $this->db->insert('users', $data);
        } else {
            $this->db->where('id', $id);
            return $this->db->update('users', $data);
        }
    }
    
    public function delete_user($id)
    {
        $this->db->where('id', $id);
        return $this->db->delete('users');
    }    
    
}
