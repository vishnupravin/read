# read



import React, { useRef, useState } from 'react'

function New() {
    let user = [{ id: 1, name: "my Name", email: 'test@ts.cm', password: 'dkfbd' },
    { id: 2, name: "delli", email: 'test2@gmail.com', password: 'test' },]

    const [count, setCount] = useState();
    const [showInput, setShowInput] = useState(false)

    const [updateState, setUpdateState] = useState()
    const [input, setInput] = useState({})
    const [wholeData, setWholeData] = useState([])
    const handleInput = (event) => {
        const lenObj = JSON.parse(localStorage.getItem('storeObj'));
        var count = 1;
        for (var item in lenObj) {
            count += lenObj[item].length
        }
        setCount(count);
        setInput({ ...input, [event.target.name]: event.target.value })

    }
    function handleSumbit() {
        input.id = wholeData.length + 1
        setWholeData([...wholeData, input])


    }
    function EditList({ current, wholeData, setWholeData }) {

        console.log({ current, wholeData, })
        function handleName(event) {

            const value = event.target.value;
            const newlist = wholeData.map((li) => (
                li.id === current.id ? { ...li, name: value } : li
            ))
            setWholeData(newlist)
        }
        function handleEmail(event) {

            const value = event.target.value;
            const newlist = wholeData.map((li) => (
                li.id === current.id ? { ...li, email: value } : li
            ))
            setWholeData(newlist)
        }
        function handlePassword(event) {

            const value = event.target.value;
            const newlist = wholeData.map((li) => (
                li.id === current.id ? { ...li, password: value } : li
            ))
            setWholeData(newlist)
        }



        return (
            <tr>
                <td><span>{wholeData[current].id}</span></td>
                <td><input type="text" name="name" value={wholeData[current].name} onChange={handleName} /></td>
                <td><input type="email" name="email" value={wholeData[current].email} onChange={handleEmail} /></td>
                <td><input type="password" name="password" value={wholeData[current].password} onChange={handlePassword} /></td>
                <td><button type="sumbit"> update</button></td>
            </tr >
        )


    }
    return (
        <div>
            {showInput ?
                <div>
                    <inpu type="hidden" name="id" value={count} onChange={handleInput} />
                    <input type="text" name="name" placeholder='ENTER UR NAME' onChange={handleInput} />
                    <input type="email" name="email" placeholder='ENTER UR EMAIL' onChange={handleInput} />
                    <input type="password" name="password" placeholder='ENTER UR PASSWORD' onChange={handleInput} />
                    <button type="sumbit" onClick={() => handleSumbit()}>NewData</button>
                    <button onClick={() => setShowInput(!showInput)} >CANCEL</button>
                </div>
                :
                <button onClick={() => setShowInput(!showInput)} >NEW DATA</button>
            }
            <button onClick={() => setWholeData([])} >CLEAR ALL</button>
            <div style={{ "height": "600px" }} >
                <form onSubmit={handleEditSumbit} >

                    <table id="customer">
                        <thead>

                            <tr>
                                <th>id</th>
                                <th>Name</th>
                                <th>email</th>
                                <th> password</th>
                                <th> update</th>
                                <th>Delete</th>
                            </tr>
                        </thead>
                        <tbody>
                            {
                                wholeData.map((current, index) => (

                                    updateState === current.id ? <EditList current={index} wholeData={wholeData} />
                                        :


                                        <tr key={index}>
                                            <td>{current.id}</td>
                                            <td>{current.name}</td>
                                            <td>{current.email}</td>
                                            <td>{current.password}</td>
                                            <td><button onClick={() => handleEdit(current.id)}>edit</button></td>
                                            <td><button onClick={() => handleDelete(current.id)}>Clear</button></td>
                                        </tr>
                                ))
                            }
                        </tbody>
                    </table>

                </form>
            </div>
        </div >

    )
    function handleEditSumbit(event) {

        const name = event.target.elements.name.value
        const email = event.target.elements.email.value
        const password = event.target.elements.password.value
        const newList = wholeData.map((li) => (
            li.id === updateState ? { ...li, name: name, email: email, password: password } : li
        ))
        setWholeData(newList)
        setUpdateState()
    }
    function handleEdit(id) {
        setUpdateState(id)

    }

    function handleDelete(id) {
        const newlist = wholeData.filter((current) => current.id !== id)
        setWholeData(newlist);
    }

}




export default New;
