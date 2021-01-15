soldity code:

pragma solidity ^0.5.0;

contract MyContract{
    string public name;
    uint public level;
    string public course;
    address owner;
    constructor() public{
        owner=msg.sender;
    }
    
    event Certificate(
        string name,
        uint level,
        string course
        );
    modifier checkLevel(uint _level){
        require(
            _level<=4,
            "Enter a valid number less than equal to 4."
            );
            _;
    }
    modifier onlyOwner{
        require(
            msg.sender==owner,
            "You must be owner to award a degree."
            );
            _;
    }
    
    function setCertificate(string memory _name, uint _level,string memory _course) checkLevel(_level) onlyOwner public{
        name=_name;
        level=_level;
        course=_course;
        emit Certificate(_name,_level,_course);
    }
    
    function getCertificate() public view returns (string memory, uint,string memory){
        return (name,level,course);
    }
  
    }
