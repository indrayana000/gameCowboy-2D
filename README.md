# kontrolPlayer-game2D

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class kontrolPlayer : MonoBehaviour
{

    public float kecepatan, scaleX, lompat;
    Animator Animation;

    // Start is called before the first frame update
    void Start()
    {
        scaleX = transform.localScale.x;
        Animation = GetComponent<Animator> ();
    }

    // Fungsi karakter berjalan ke kiri
    public void jalan_kiri(){

        // Mengambil animasi
       if (Animation.GetCurrentAnimatorStateInfo (0).IsName ("New State")){
            Animation.SetTrigger ("jalan");
        }
        transform.localScale = new Vector3 (-scaleX, transform.localScale.y, transform.localScale.z);
        transform.Translate (Vector3.left*kecepatan*Time.fixedDeltaTime, Space.Self);
    }

    // Fungsi karakter berjalan ke kanan
    public void jalan_kanan(){

        // Mengambil animasi
        if (Animation.GetCurrentAnimatorStateInfo (0).IsName ("New State")){
            Animation.SetTrigger ("jalan");
        }
        transform.localScale = new Vector3 (scaleX, transform.localScale.y, transform.localScale.z);
        transform.Translate (Vector3.right*kecepatan*Time.fixedDeltaTime, Space.Self);
    }

    public void melompat(){
        GetComponent<Rigidbody2D> ().velocity = new Vector2 (0, lompat);
    }

    // Fungsi berhenti pada animator
    public void berhenti(){
        Animation.SetTrigger ("stop");
    }

    // Update is called once per frame
    void Update()
    {
        // karakter berjalan
        if(Input.GetKey (KeyCode.LeftArrow)){
            jalan_kiri();
        }
        if(Input.GetKey (KeyCode.RightArrow)){
            jalan_kanan();
        }

        // karakter melompat
        if(Input.GetKeyDown(KeyCode.UpArrow)){
            melompat();
        }

        // karakter berhenti pada animator
         if(Input.GetKeyUp (KeyCode.LeftArrow)){
            berhenti();
        }
        if(Input.GetKeyUp (KeyCode.RightArrow)){
            berhenti();
        }
    }
}
