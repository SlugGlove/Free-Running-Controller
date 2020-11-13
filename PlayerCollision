using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerCollision : MonoBehaviour
{
    public float FloorCheckRadius; //how large the detection for the floors is
    public float bottomOffset; //offset from player centre
    public float WallCheckRadius; //how large the detection for the walls is
    public float frontOffset; //offset from the players centre 
    public float RoofCheckRadius; //the amount we check before standing up 
    public float upOffset; //offset upwards

    public float LedgeGrabForwardPos; //the position in front of the player where we check for ledges
    public float LedgeGrabUpwardsPos;//the position in above of the player where we check for ledges
    public float LedgeGrabDistance; //the distance the ledge can be from our raycast before we grab it (this is projects from the top of the wall grab position, downwards

    public LayerMask FloorLayers; //what layers we can stand on
    public LayerMask WallLayers;  //what layers we can wall run on
    public LayerMask RoofLayers; //what layers we cannot stand up under (for crouching
    public LayerMask LedgeGrabLayers; //what layers we will grab onto

    //check if there is floor below us
    public bool CheckFloor(Vector3 Direction)
    {
        Vector3 Pos = transform.position + (Direction * bottomOffset);
        Collider[] hitColliders = Physics.OverlapSphere(Pos, FloorCheckRadius, FloorLayers);
        if (hitColliders.Length > 0)
        {
            //we are on the ground
            return true;
        }

        return false;
    }
    //check if there is a wall in the direction we are pressing
    public bool CheckWall(Vector3 Direction)
    {
        Vector3 Pos = transform.position + (Direction * frontOffset);
        Collider[] hitColliders = Physics.OverlapSphere(Pos, WallCheckRadius, WallLayers);
        if (hitColliders.Length > 0)
        {
            //we are on the ground
            return true;
        }

        return false;
    }
    //check there is nothing above our head so we can stand up
    public bool CheckRoof(Vector3 Direction)
    {
        Vector3 Pos = transform.position + (Direction * upOffset);
        Collider[] hitColliders = Physics.OverlapSphere(Pos, WallCheckRadius, RoofLayers);
        if (hitColliders.Length > 0)
        {
            //we are on the ground
            return true;
        }

        return false;
    }

    public Vector3 CheckLedges()
    {
        Vector3 RayPos = transform.position + (transform.forward * LedgeGrabForwardPos) + (transform.up * LedgeGrabUpwardsPos);

        RaycastHit hit;
        if (Physics.Raycast(RayPos, -transform.up, out hit, LedgeGrabDistance, LedgeGrabLayers))
            return hit.point;


        return Vector3.zero;
    }

    void OnDrawGizmosSelected()
    {
        //floor check
        Gizmos.color = Color.yellow;
        Vector3 Pos = transform.position + (-transform.up * bottomOffset);
        Gizmos.DrawSphere(Pos, FloorCheckRadius);
        //wall check
        Gizmos.color = Color.red;
        Vector3 Pos2 = transform.position + (transform.forward * frontOffset);
        Gizmos.DrawSphere(Pos2, WallCheckRadius);
        //roof check
        Gizmos.color = Color.green;
        Vector3 Pos3 = transform.position + (transform.up * upOffset);
        Gizmos.DrawSphere(Pos3, RoofCheckRadius);
        //Ledge check
        Gizmos.color = Color.black;
        Vector3 Pos4 = transform.position + (transform.forward * LedgeGrabForwardPos) + (transform.up * LedgeGrabUpwardsPos);
        Gizmos.DrawLine(Pos4, Pos4 + (-transform.up * LedgeGrabDistance));
    }
}
