# React and Javascript Cheatsheet

In these examples, I am using MUI Material UI as the main React Component Library.

Contents:
- [`useState` Hooks with React](#usestate-hooks-with-react)
- [React Swipeable Views React 18 Fix](#react-swipeable-views-react-18-fix)

***
### `useState` Hooks with React

```js
import { useState } from "react";
import { Button, Typography } from '@mui/material';

function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count => count + 1);
  }

  return (
    <>
      <Typography>{count} times</Typography>
      <Button onClick={handleClick}>Add 1</Button>
    </>
  );
}
```

### React Swipeable Views React 18 Fix
If you decide to use React 18+ and want to use the package `react-swipeable-views`, you may have realised that you encounter an error when trying to install the package. Thankfully, their is a fix for this within a package called `react-swipeable-views-react-18-fix`.
This is a direct fix for [React Stepper Component - Material UI](https://mui.com/material-ui/react-stepper/#text-with-carousel-effect).

```js
import ArrowLeftIcon from '@heroicons/react/24/solid/ArrowLeftIcon';
import ArrowRightIcon from '@heroicons/react/24/solid/ArrowRightIcon';
import { useTheme, Box, Button, MobileStepper, Paper, Typography } from "@mui/material";
import { useState } from 'react';

import SwipeableViews from "react-swipeable-views-react-18-fix"
import { autoPlay } from 'react-swipeable-views-utils-react-18-fix';

const AutoPlaySwipeableViews = autoPlay(SwipeableViews);

const images = [
  {
    label: 'San Francisco – Oakland Bay Bridge, United States',
    imgPath:
      'https://images.unsplash.com/photo-1537944434965-cf4679d1a598?auto=format&fit=crop&w=400&h=250&q=60',
  },
  {
    label: 'Bird',
    imgPath:
      'https://images.unsplash.com/photo-1538032746644-0212e812a9e7?auto=format&fit=crop&w=400&h=250&q=60',
  },
  {
    label: 'Bali, Indonesia',
    imgPath:
      'https://images.unsplash.com/photo-1537996194471-e657df975ab4?auto=format&fit=crop&w=400&h=250',
  },
  {
    label: 'Goč, Serbia',
    imgPath:
      'https://images.unsplash.com/photo-1512341689857-198e7e2f3ca8?auto=format&fit=crop&w=400&h=250&q=60',
  },
];

function SwipeableTextMobileStepper() {
  const theme = useTheme();
  const [activeStep, setActiveStep] = useState(0);
  const maxSteps = images.length;

  const handleNext = () => {
    setActiveStep((prevActiveStep) => prevActiveStep + 1);
  };

  const handleBack = () => {
    setActiveStep((prevActiveStep) => prevActiveStep - 1);
  };

  const handleStepChange = (step) => {
    setActiveStep(step);
  };

  return (
    <Box sx={{ maxWidth: 400, flexGrow: 1 }}>
      <Paper
        square
        elevation={0}
        sx={{
          display: 'flex',
          alignItems: 'center',
          height: 50,
          pl: 2,
          bgcolor: 'background.default',
        }}
      >
        <Typography>{images[activeStep].label}</Typography>
      </Paper>
      <AutoPlaySwipeableViews
        axis={theme.direction === 'rtl' ? 'x-reverse' : 'x'}
        index={activeStep}
        onChangeIndex={handleStepChange}
        enableMouseEvents
      >
        {images.map((step, index) => (
          <div key={step.label}>
            {Math.abs(activeStep - index) <= 2 ? (
              <Box
                component="img"
                sx={{
                  height: 255,
                  display: 'block',
                  maxWidth: 400,
                  overflow: 'hidden',
                  width: '100%',
                }}
                src={step.imgPath}
                alt={step.label}
              />
            ) : null}
          </div>
        ))}
      </AutoPlaySwipeableViews>
      <MobileStepper
        steps={maxSteps}
        position="static"
        activeStep={activeStep}
        nextButton={
          <Button
            size="small"
            onClick={handleNext}
            disabled={activeStep === maxSteps - 1}
          >
            Next
            {theme.direction === 'rtl' ? (
              <ArrowLeftIcon />
            ) : (
              <ArrowRightIcon />
            )}
          </Button>
        }
        backButton={
          <Button size="small" onClick={handleBack} disabled={activeStep === 0}>
            {theme.direction === 'rtl' ? (
              <ArrowRightIcon />
            ) : (
              <ArrowLeftIcon />
            )}
            Back
          </Button>
        }
      />
    </Box>
  );
}

```

***
