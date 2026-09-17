using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    public float forwardSpeed = 7f;
    public float sideSpeed = 6f;

    void Update()
    {
        // Left / Right movement
        float side = Input.GetAxis("Horizontal");

        // Automatically forward + Left/Right
        Vector3 movement = new Vector3(
            side * sideSpeed,
            0f,
            forwardSpeed
        );

        transform.Translate(movement * Time.deltaTime, Space.World);
    }
}
