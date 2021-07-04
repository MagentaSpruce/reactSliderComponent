# reactSliderComponent
This React project consist of an  auto-slider component.

This component can be easily utilized across applications and purposes with minimal edits required.

A brief overview of the pertinent React code is given below:

To begin the state values were set up to monitor the data and the index where the data will begin at.
```React
function App() {
  const [people, setPeople] = useState(data);
  const [index, setIndex] = useState(0);
  ...
  ```
  
  The return was then formatted. The first return is used to gather and retrieve the data objects. To do this the data is iterated over and deconstructed using .map(). The 2nd return is what renders each object onto the screen.
  ```React
  return (
    <section className="section">
      <div className="title">
        <h2>
          <span>/</span>reviews
        </h2>
      </div>
      <div className="section-center">
        {people.map((person, personIndex) => {
          const { id, image, name, title, quote } = person;
          
          return (
            <article key={id}>
              <img src={image} alt={name} className="person-img" />
              <h4>{name}</h4>
              <p className="title">{title}</p>
              <p className="text">{quote}</p>
              <FaQuoteRight className="icon" />
            </article>
          );
        })}
        <button className="prev">
          <FiChevronLeft />
        </button>
        <button className="next">
          <FiChevronRight />
        </button>
      </div>
    </section>
  );
}
```

Due to CSS properties the data is all stacked on top of itself on the page. The slides are moved by way of changing their class settings (lastSlide, activeSlide, nextSlide). The classes changes with the changing value of the index. Only the active slides receive opacity of 1, the rest are hidden.
The classes are added when iterating over the list and by default all the slides receive the nextSlide position which renders them all to the right side of the page. 
```React
       let position = "nextSlide";
       ```
       
   Now to set up the active slide the index is checked. If the personIndex value is equal to the index value then the active class is applied.
   ```React
            if (personIndex === index) {
            position = "activeSlide";
          }
    ```
    
    This places the active slide in the center. Now to apply the lastSlide class:
    ```React
              if (
            personIndex === index - 1 ||
            (index === 0 && personIndex === people.length - 1)
          ) {
            position = "lastSlide";
          }
   ```
   
   Now the button functionality is added to control the state of the index. 
   ```React
           <button className="prev" onClick={() => setIndex(index - 1)}>
          <FiChevronLeft />
        </button>
        <button className="next" onClick={() => setIndex(index + 1)}>
          <FiChevronRight />
        </button>
  ```
  
  
  To prevent bugs when the [] ends is reached, either forwards or backwards, useEffect() is used to reset the slider as needed.
  ```React
    useEffect(() => {
    const lastIndex = people.length - 1;
    if (index < 0) {
      setIndex(lastIndex);
    }
    if (index > lastIndex) {
      setIndex(0);
    }
  }, [index, people]);
  ```
  
  One more use affect is set up for the auto-slide functionality. To remove the active class from non-active elements that were previously clicked and have the interval timer set a the clearInterval() function is used. This ensures only the active slide has a timer set, no other slides.
  ```React
    useEffect(() => {
    let slider = setInterval(() => {
      setIndex(index + 1);
    }, 3500);
    return () => clearInterval(slider);
  }, [index]);
  ```
  
  Lastly, render to the screen.
  ```React
  ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

***End walkthrough
  
   
    
   
